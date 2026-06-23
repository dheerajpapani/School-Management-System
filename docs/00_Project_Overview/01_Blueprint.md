## 1) FULL DATABASE SCHEMA (MySQL 8.0+)

```sql
CREATE DATABASE IF NOT EXISTS sms_db
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;

USE sms_db;

SET FOREIGN_KEY_CHECKS = 0;

-- =========================
-- CORE / CONFIG / SECURITY
-- =========================

CREATE TABLE IF NOT EXISTS sms_institutions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(191) NOT NULL,
  code VARCHAR(50) NOT NULL,
  address TEXT NULL,
  email VARCHAR(191) NULL,
  phone VARCHAR(30) NULL,
  website VARCHAR(191) NULL,
  logo_path VARCHAR(255) NULL,
  timezone VARCHAR(64) NOT NULL DEFAULT 'Asia/Kolkata',
  currency_code CHAR(3) NOT NULL DEFAULT 'INR',
  academic_year_start_month TINYINT UNSIGNED NOT NULL DEFAULT 4,
  academic_year_start_day TINYINT UNSIGNED NOT NULL DEFAULT 1,
  settings JSON NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_institution_code (code)
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_branches (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  institution_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(191) NOT NULL,
  code VARCHAR(50) NOT NULL,
  address TEXT NULL,
  phone VARCHAR(30) NULL,
  email VARCHAR(191) NULL,
  is_main TINYINT(1) NOT NULL DEFAULT 0,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_branch_code (code),
  KEY idx_branch_institution (institution_id),
  CONSTRAINT fk_branch_institution
    FOREIGN KEY (institution_id) REFERENCES sms_institutions(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_settings (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NULL,
  setting_group VARCHAR(100) NOT NULL,
  setting_key VARCHAR(100) NOT NULL,
  setting_value JSON NOT NULL,
  value_type ENUM('string','number','boolean','json','date','datetime') NOT NULL DEFAULT 'string',
  is_system TINYINT(1) NOT NULL DEFAULT 0,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_settings_scope (branch_id, setting_group, setting_key),
  KEY idx_settings_group (setting_group),
  CONSTRAINT fk_settings_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_users (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(100) NOT NULL,
  email VARCHAR(191) NULL,
  phone VARCHAR(30) NULL,
  password_hash VARCHAR(255) NOT NULL,
  user_type ENUM('student','parent','teacher','staff','admin','alumni','system') NOT NULL,
  status ENUM('pending','active','inactive','blocked') NOT NULL DEFAULT 'active',
  email_verified_at DATETIME NULL,
  phone_verified_at DATETIME NULL,
  last_login_at DATETIME NULL,
  last_login_ip VARCHAR(45) NULL,
  remember_token VARCHAR(100) NULL,
  deleted_at DATETIME NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_users_username (username),
  UNIQUE KEY uq_users_email (email),
  UNIQUE KEY uq_users_phone (phone),
  KEY idx_users_type_status (user_type, status)
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_roles (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  slug VARCHAR(100) NOT NULL,
  description VARCHAR(255) NULL,
  is_system TINYINT(1) NOT NULL DEFAULT 0,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_roles_slug (slug)
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_permissions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  module_name VARCHAR(100) NOT NULL,
  controller_name VARCHAR(100) NOT NULL,
  action_name VARCHAR(100) NOT NULL,
  permission_key VARCHAR(191) NOT NULL,
  description VARCHAR(255) NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_permission_key (permission_key),
  KEY idx_permission_module (module_name, controller_name, action_name)
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_role_permissions (
  role_id BIGINT UNSIGNED NOT NULL,
  permission_id BIGINT UNSIGNED NOT NULL,
  granted_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (role_id, permission_id),
  CONSTRAINT fk_rp_role
    FOREIGN KEY (role_id) REFERENCES sms_roles(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_rp_permission
    FOREIGN KEY (permission_id) REFERENCES sms_permissions(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_user_roles (
  user_id BIGINT UNSIGNED NOT NULL,
  role_id BIGINT UNSIGNED NOT NULL,
  scope_type ENUM('global','branch','class','section') NOT NULL DEFAULT 'global',
  scope_id BIGINT UNSIGNED NULL,
  assigned_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (user_id, role_id, scope_type, scope_id),
  KEY idx_user_roles_role (role_id),
  CONSTRAINT fk_ur_user
    FOREIGN KEY (user_id) REFERENCES sms_users(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_ur_role
    FOREIGN KEY (role_id) REFERENCES sms_roles(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_menu_items (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  parent_id BIGINT UNSIGNED NULL,
  permission_id BIGINT UNSIGNED NULL,
  label VARCHAR(100) NOT NULL,
  route VARCHAR(191) NULL,
  icon VARCHAR(100) NULL,
  sort_order INT NOT NULL DEFAULT 0,
  is_active TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  KEY idx_menu_parent (parent_id),
  KEY idx_menu_permission (permission_id),
  CONSTRAINT fk_menu_parent
    FOREIGN KEY (parent_id) REFERENCES sms_menu_items(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_menu_permission
    FOREIGN KEY (permission_id) REFERENCES sms_permissions(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_audit_logs (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  user_id BIGINT UNSIGNED NULL,
  action VARCHAR(100) NOT NULL,
  entity_type VARCHAR(100) NOT NULL,
  entity_id BIGINT UNSIGNED NULL,
  old_values JSON NULL,
  new_values JSON NULL,
  ip_address VARCHAR(45) NULL,
  user_agent VARCHAR(255) NULL,
  http_method VARCHAR(10) NULL,
  request_uri VARCHAR(255) NULL,
  status_code SMALLINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  KEY idx_audit_entity (entity_type, entity_id),
  KEY idx_audit_user (user_id),
  CONSTRAINT fk_audit_user
    FOREIGN KEY (user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_file_uploads (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  entity_type VARCHAR(100) NOT NULL,
  entity_id BIGINT UNSIGNED NOT NULL,
  uploaded_by BIGINT UNSIGNED NULL,
  file_name VARCHAR(255) NOT NULL,
  file_path VARCHAR(255) NOT NULL,
  mime_type VARCHAR(100) NULL,
  file_size BIGINT UNSIGNED NULL,
  file_hash CHAR(64) NULL,
  is_public TINYINT(1) NOT NULL DEFAULT 0,
  metadata JSON NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  KEY idx_file_entity (entity_type, entity_id),
  KEY idx_file_uploader (uploaded_by),
  CONSTRAINT fk_file_uploader
    FOREIGN KEY (uploaded_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- ACADEMIC STRUCTURE
-- =========================

CREATE TABLE IF NOT EXISTS sms_academic_years (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(50) NOT NULL,
  start_date DATE NOT NULL,
  end_date DATE NOT NULL,
  is_current TINYINT(1) NOT NULL DEFAULT 0,
  status ENUM('active','closed') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_year_branch_name (branch_id, name),
  KEY idx_year_branch (branch_id),
  CONSTRAINT fk_year_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_academic_terms (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(50) NOT NULL,
  term_type ENUM('term','semester','quarter') NOT NULL DEFAULT 'term',
  start_date DATE NOT NULL,
  end_date DATE NOT NULL,
  sort_order INT NOT NULL DEFAULT 0,
  is_active TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_term_year_name (academic_year_id, name),
  KEY idx_term_year (academic_year_id),
  CONSTRAINT fk_term_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_working_days (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  day_of_week TINYINT UNSIGNED NOT NULL, -- 1=Mon ... 7=Sun
  is_working TINYINT(1) NOT NULL DEFAULT 1,
  start_time TIME NULL,
  end_time TIME NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_working_day (branch_id, day_of_week),
  CONSTRAINT fk_working_days_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_grading_systems (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  scheme_type ENUM('marks','gpa','cgpa') NOT NULL DEFAULT 'marks',
  min_pass_percentage DECIMAL(5,2) NOT NULL DEFAULT 35.00,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_grade_system (branch_id, name),
  CONSTRAINT fk_grade_system_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_grade_scales (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  grading_system_id BIGINT UNSIGNED NOT NULL,
  min_mark DECIMAL(6,2) NOT NULL,
  max_mark DECIMAL(6,2) NOT NULL,
  grade_label VARCHAR(10) NOT NULL,
  grade_point DECIMAL(4,2) NOT NULL DEFAULT 0.00,
  remarks VARCHAR(255) NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_grade_band (grading_system_id, min_mark, max_mark),
  CONSTRAINT fk_grade_scale_system
    FOREIGN KEY (grading_system_id) REFERENCES sms_grading_systems(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_departments (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  code VARCHAR(50) NOT NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_department_code (branch_id, code),
  CONSTRAINT fk_department_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_classes (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  department_id BIGINT UNSIGNED NULL,
  name VARCHAR(100) NOT NULL,
  code VARCHAR(50) NOT NULL,
  sort_order INT NOT NULL DEFAULT 0,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_class_code (branch_id, academic_year_id, code),
  KEY idx_class_year (academic_year_id),
  CONSTRAINT fk_class_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_class_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_class_department
    FOREIGN KEY (department_id) REFERENCES sms_departments(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_sections (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  class_id BIGINT UNSIGNED NOT NULL,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(50) NOT NULL,
  capacity INT UNSIGNED NOT NULL DEFAULT 40,
  homeroom_teacher_id BIGINT UNSIGNED NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_section_class_name (class_id, name),
  CONSTRAINT fk_section_class
    FOREIGN KEY (class_id) REFERENCES sms_classes(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_section_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_section_teacher
    FOREIGN KEY (homeroom_teacher_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_rooms (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  building_name VARCHAR(100) NULL,
  room_no VARCHAR(50) NOT NULL,
  room_type ENUM('classroom','lab','exam_room','office','hostel','other') NOT NULL DEFAULT 'classroom',
  capacity INT UNSIGNED NOT NULL DEFAULT 40,
  floor_no INT NULL,
  is_active TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_room (branch_id, room_no),
  CONSTRAINT fk_room_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_houses (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  color VARCHAR(30) NULL,
  captain_user_id BIGINT UNSIGNED NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_house (branch_id, name),
  CONSTRAINT fk_house_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_house_captain
    FOREIGN KEY (captain_user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_clubs (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  description TEXT NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_club (branch_id, name),
  CONSTRAINT fk_club_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_committees (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  description TEXT NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_committee (branch_id, name),
  CONSTRAINT fk_committee_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- STAFF / TEACHERS / EMPLOYEES
-- =========================

CREATE TABLE IF NOT EXISTS sms_employees (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  user_id BIGINT UNSIGNED NULL,
  branch_id BIGINT UNSIGNED NOT NULL,
  department_id BIGINT UNSIGNED NULL,
  employee_code VARCHAR(50) NOT NULL,
  employee_type ENUM('teacher','staff','admin') NOT NULL DEFAULT 'staff',
  designation VARCHAR(100) NULL,
  qualification VARCHAR(191) NULL,
  specialization VARCHAR(191) NULL,
  joining_date DATE NULL,
  salary DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  status ENUM('active','inactive','left') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_employee_code (branch_id, employee_code),
  KEY idx_employee_user (user_id),
  CONSTRAINT fk_employee_user
    FOREIGN KEY (user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_employee_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_employee_department
    FOREIGN KEY (department_id) REFERENCES sms_departments(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_employee_leaves (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  employee_id BIGINT UNSIGNED NOT NULL,
  leave_type VARCHAR(50) NOT NULL,
  start_date DATE NOT NULL,
  end_date DATE NOT NULL,
  reason TEXT NULL,
  status ENUM('pending','approved','rejected','cancelled') NOT NULL DEFAULT 'pending',
  approved_by BIGINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  KEY idx_leave_employee (employee_id),
  CONSTRAINT fk_leave_employee
    FOREIGN KEY (employee_id) REFERENCES sms_employees(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_leave_approver
    FOREIGN KEY (approved_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- SUBJECTS / CURRICULUM / LESSON PLANS
-- =========================

CREATE TABLE IF NOT EXISTS sms_subject_categories (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_subject_cat (branch_id, name),
  CONSTRAINT fk_subject_cat_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_subjects (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  category_id BIGINT UNSIGNED NULL,
  code VARCHAR(50) NOT NULL,
  name VARCHAR(100) NOT NULL,
  subject_type ENUM('core','elective','optional','lab') NOT NULL DEFAULT 'core',
  credit_hours DECIMAL(4,1) NOT NULL DEFAULT 1.0,
  min_pass_marks DECIMAL(6,2) NOT NULL DEFAULT 35.00,
  max_marks DECIMAL(6,2) NOT NULL DEFAULT 100.00,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_subject_code (branch_id, code),
  KEY idx_subject_name (name),
  CONSTRAINT fk_subject_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_subject_category
    FOREIGN KEY (category_id) REFERENCES sms_subject_categories(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_teacher_subjects (
  teacher_id BIGINT UNSIGNED NOT NULL,
  subject_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (teacher_id, subject_id, academic_year_id),
  CONSTRAINT fk_teacher_subject_teacher
    FOREIGN KEY (teacher_id) REFERENCES sms_employees(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_teacher_subject_subject
    FOREIGN KEY (subject_id) REFERENCES sms_subjects(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_teacher_subject_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_class_subjects (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  class_id BIGINT UNSIGNED NOT NULL,
  section_id BIGINT UNSIGNED NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  subject_id BIGINT UNSIGNED NOT NULL,
  teacher_id BIGINT UNSIGNED NULL,
  room_id BIGINT UNSIGNED NULL,
  is_elective TINYINT(1) NOT NULL DEFAULT 0,
  is_optional TINYINT(1) NOT NULL DEFAULT 0,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_class_subject (class_id, section_id, academic_year_id, subject_id),
  CONSTRAINT fk_class_subject_class
    FOREIGN KEY (class_id) REFERENCES sms_classes(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_class_subject_section
    FOREIGN KEY (section_id) REFERENCES sms_sections(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_class_subject_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_class_subject_subject
    FOREIGN KEY (subject_id) REFERENCES sms_subjects(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_class_subject_teacher
    FOREIGN KEY (teacher_id) REFERENCES sms_employees(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_class_subject_room
    FOREIGN KEY (room_id) REFERENCES sms_rooms(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_curricula (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  class_id BIGINT UNSIGNED NOT NULL,
  subject_id BIGINT UNSIGNED NOT NULL,
  syllabus_version VARCHAR(50) NOT NULL,
  description TEXT NULL,
  meta JSON NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_curriculum (academic_year_id, class_id, subject_id, syllabus_version),
  CONSTRAINT fk_curriculum_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_curriculum_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_curriculum_class
    FOREIGN KEY (class_id) REFERENCES sms_classes(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_curriculum_subject
    FOREIGN KEY (subject_id) REFERENCES sms_subjects(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_learning_outcomes (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  curriculum_id BIGINT UNSIGNED NOT NULL,
  title VARCHAR(191) NOT NULL,
  description TEXT NULL,
  sort_order INT NOT NULL DEFAULT 0,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_lo_curriculum
    FOREIGN KEY (curriculum_id) REFERENCES sms_curricula(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_lesson_plans (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  teacher_id BIGINT UNSIGNED NOT NULL,
  class_subject_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  term_id BIGINT UNSIGNED NULL,
  plan_date DATE NOT NULL,
  topic VARCHAR(191) NOT NULL,
  objectives TEXT NULL,
  content JSON NULL,
  progress_percentage DECIMAL(5,2) NOT NULL DEFAULT 0.00,
  status ENUM('draft','submitted','approved','rejected') NOT NULL DEFAULT 'draft',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  KEY idx_lesson_plan_date (plan_date),
  CONSTRAINT fk_lesson_teacher
    FOREIGN KEY (teacher_id) REFERENCES sms_employees(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_lesson_class_subject
    FOREIGN KEY (class_subject_id) REFERENCES sms_class_subjects(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_lesson_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_lesson_term
    FOREIGN KEY (term_id) REFERENCES sms_academic_terms(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- STUDENT / GUARDIAN / ADMISSION
-- =========================

CREATE TABLE IF NOT EXISTS sms_admission_enquiries (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  parent_name VARCHAR(191) NOT NULL,
  student_name VARCHAR(191) NOT NULL,
  desired_class_id BIGINT UNSIGNED NULL,
  phone VARCHAR(30) NULL,
  email VARCHAR(191) NULL,
  notes TEXT NULL,
  status ENUM('open','converted','closed') NOT NULL DEFAULT 'open',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  KEY idx_enquiry_phone (phone),
  CONSTRAINT fk_enquiry_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_enquiry_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_enquiry_class
    FOREIGN KEY (desired_class_id) REFERENCES sms_classes(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_admission_applications (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  enquiry_id BIGINT UNSIGNED NULL,
  application_no VARCHAR(50) NOT NULL,
  branch_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  applied_class_id BIGINT UNSIGNED NOT NULL,
  applicant_json JSON NOT NULL,
  documents_json JSON NULL,
  status ENUM('draft','submitted','under_review','shortlisted','rejected','approved') NOT NULL DEFAULT 'submitted',
  submitted_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_application_no (application_no),
  CONSTRAINT fk_application_enquiry
    FOREIGN KEY (enquiry_id) REFERENCES sms_admission_enquiries(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_application_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_application_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_application_class
    FOREIGN KEY (applied_class_id) REFERENCES sms_classes(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_admission_tests (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  application_id BIGINT UNSIGNED NOT NULL,
  test_date DATE NOT NULL,
  score DECIMAL(6,2) NULL,
  max_score DECIMAL(6,2) NOT NULL DEFAULT 100.00,
  remarks TEXT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_test_application
    FOREIGN KEY (application_id) REFERENCES sms_admission_applications(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_admission_interviews (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  application_id BIGINT UNSIGNED NOT NULL,
  interviewer_user_id BIGINT UNSIGNED NULL,
  schedule_at DATETIME NOT NULL,
  result ENUM('pending','pass','fail') NOT NULL DEFAULT 'pending',
  remarks TEXT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_interview_application
    FOREIGN KEY (application_id) REFERENCES sms_admission_applications(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_interview_user
    FOREIGN KEY (interviewer_user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_admission_approvals (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  application_id BIGINT UNSIGNED NOT NULL,
  approved_by BIGINT UNSIGNED NULL,
  decision ENUM('approved','rejected','waitlisted') NOT NULL,
  decision_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  remarks TEXT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_approval_application
    FOREIGN KEY (application_id) REFERENCES sms_admission_applications(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_approval_user
    FOREIGN KEY (approved_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_students (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  user_id BIGINT UNSIGNED NULL,
  branch_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  current_class_id BIGINT UNSIGNED NOT NULL,
  current_section_id BIGINT UNSIGNED NULL,
  current_house_id BIGINT UNSIGNED NULL,
  hostel_id BIGINT UNSIGNED NULL,
  transport_assignment_id BIGINT UNSIGNED NULL,
  admission_no VARCHAR(50) NOT NULL,
  roll_no VARCHAR(50) NULL,
  first_name VARCHAR(100) NOT NULL,
  middle_name VARCHAR(100) NULL,
  last_name VARCHAR(100) NULL,
  dob DATE NOT NULL,
  gender ENUM('male','female','other') NOT NULL,
  blood_group VARCHAR(10) NULL,
  religion VARCHAR(50) NULL,
  nationality VARCHAR(50) NULL DEFAULT 'Indian',
  category VARCHAR(50) NULL,
  aadhaar_no VARCHAR(20) NULL,
  admission_date DATE NOT NULL,
  photo_path VARCHAR(255) NULL,
  status ENUM('admitted','active','promoted','transferred','graduated','left','suspended') NOT NULL DEFAULT 'active',
  created_by BIGINT UNSIGNED NULL,
  deleted_at DATETIME NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_student_admission_no (admission_no),
  UNIQUE KEY uq_student_roll (branch_id, academic_year_id, roll_no),
  KEY idx_student_class_section (current_class_id, current_section_id),
  KEY idx_student_user (user_id),
  CONSTRAINT fk_student_user
    FOREIGN KEY (user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_student_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_student_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_student_class
    FOREIGN KEY (current_class_id) REFERENCES sms_classes(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_student_section
    FOREIGN KEY (current_section_id) REFERENCES sms_sections(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_student_house
    FOREIGN KEY (current_house_id) REFERENCES sms_houses(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_guardians (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  user_id BIGINT UNSIGNED NULL,
  name VARCHAR(191) NOT NULL,
  relation ENUM('father','mother','guardian','spouse','other') NOT NULL DEFAULT 'guardian',
  phone VARCHAR(30) NULL,
  email VARCHAR(191) NULL,
  occupation VARCHAR(100) NULL,
  address TEXT NULL,
  is_primary TINYINT(1) NOT NULL DEFAULT 0,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  KEY idx_guardian_user (user_id),
  CONSTRAINT fk_guardian_user
    FOREIGN KEY (user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_student_guardians (
  student_id BIGINT UNSIGNED NOT NULL,
  guardian_id BIGINT UNSIGNED NOT NULL,
  is_primary TINYINT(1) NOT NULL DEFAULT 0,
  is_emergency TINYINT(1) NOT NULL DEFAULT 0,
  pickup_rights TINYINT(1) NOT NULL DEFAULT 0,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (student_id, guardian_id),
  CONSTRAINT fk_sg_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_sg_guardian
    FOREIGN KEY (guardian_id) REFERENCES sms_guardians(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_student_documents (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  document_type VARCHAR(100) NOT NULL,
  document_name VARCHAR(191) NOT NULL,
  file_path VARCHAR(255) NOT NULL,
  file_hash CHAR(64) NULL,
  verified_by BIGINT UNSIGNED NULL,
  verified_at DATETIME NULL,
  status ENUM('pending','verified','rejected') NOT NULL DEFAULT 'pending',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  KEY idx_student_doc_student (student_id),
  CONSTRAINT fk_doc_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_doc_verified_by
    FOREIGN KEY (verified_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_student_lifecycle_events (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  event_type ENUM('admission','promotion','section_transfer','branch_transfer','graduation','alumni_conversion','exit') NOT NULL,
  from_class_id BIGINT UNSIGNED NULL,
  from_section_id BIGINT UNSIGNED NULL,
  to_class_id BIGINT UNSIGNED NULL,
  to_section_id BIGINT UNSIGNED NULL,
  effective_date DATE NOT NULL,
  remarks TEXT NULL,
  payload JSON NULL,
  created_by BIGINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  KEY idx_lifecycle_student (student_id),
  CONSTRAINT fk_lifecycle_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_lifecycle_from_class
    FOREIGN KEY (from_class_id) REFERENCES sms_classes(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_lifecycle_from_section
    FOREIGN KEY (from_section_id) REFERENCES sms_sections(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_lifecycle_to_class
    FOREIGN KEY (to_class_id) REFERENCES sms_classes(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_lifecycle_to_section
    FOREIGN KEY (to_section_id) REFERENCES sms_sections(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_lifecycle_creator
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- ATTENDANCE
-- =========================

CREATE TABLE IF NOT EXISTS sms_attendance_sessions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  attendance_scope ENUM('student','staff') NOT NULL DEFAULT 'student',
  scope_type ENUM('class','section','subject','all') NOT NULL DEFAULT 'class',
  class_id BIGINT UNSIGNED NULL,
  section_id BIGINT UNSIGNED NULL,
  subject_id BIGINT UNSIGNED NULL,
  attendance_date DATE NOT NULL,
  period_no INT NULL,
  taken_by BIGINT UNSIGNED NULL,
  marked_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  status ENUM('draft','finalized') NOT NULL DEFAULT 'finalized',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  KEY idx_att_session_date (attendance_date),
  UNIQUE KEY uq_att_session (attendance_scope, scope_type, class_id, section_id, subject_id, attendance_date, period_no),
  CONSTRAINT fk_att_session_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_att_session_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_att_session_class
    FOREIGN KEY (class_id) REFERENCES sms_classes(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_att_session_section
    FOREIGN KEY (section_id) REFERENCES sms_sections(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_att_session_subject
    FOREIGN KEY (subject_id) REFERENCES sms_subjects(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_att_session_user
    FOREIGN KEY (taken_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_student_attendance (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  session_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  status ENUM('present','absent','late','excused') NOT NULL DEFAULT 'present',
  reason VARCHAR(255) NULL,
  marked_by BIGINT UNSIGNED NULL,
  marked_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_student_attendance (session_id, student_id),
  CONSTRAINT fk_sa_session
    FOREIGN KEY (session_id) REFERENCES sms_attendance_sessions(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_sa_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_sa_marked_by
    FOREIGN KEY (marked_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_staff_attendance (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  employee_id BIGINT UNSIGNED NOT NULL,
  attendance_date DATE NOT NULL,
  shift_name VARCHAR(50) NULL,
  status ENUM('present','absent','late','half_day','excused') NOT NULL DEFAULT 'present',
  in_time TIME NULL,
  out_time TIME NULL,
  overtime_minutes INT UNSIGNED NOT NULL DEFAULT 0,
  marked_by BIGINT UNSIGNED NULL,
  marked_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_staff_att (employee_id, attendance_date, shift_name),
  CONSTRAINT fk_staff_att_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_staff_att_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_staff_att_employee
    FOREIGN KEY (employee_id) REFERENCES sms_employees(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_staff_att_marked_by
    FOREIGN KEY (marked_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- EXAM / ASSESSMENT / REPORT CARDS
-- =========================

CREATE TABLE IF NOT EXISTS sms_exam_types (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  code VARCHAR(50) NOT NULL,
  is_termly TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_exam_type_code (branch_id, code),
  CONSTRAINT fk_exam_type_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_exams (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  exam_type_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  term_id BIGINT UNSIGNED NULL,
  name VARCHAR(191) NOT NULL,
  start_date DATE NOT NULL,
  end_date DATE NOT NULL,
  max_marks_per_subject DECIMAL(6,2) NOT NULL DEFAULT 100.00,
  status ENUM('draft','scheduled','running','completed','published') NOT NULL DEFAULT 'draft',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  CONSTRAINT fk_exam_type
    FOREIGN KEY (exam_type_id) REFERENCES sms_exam_types(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_exam_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_exam_term
    FOREIGN KEY (term_id) REFERENCES sms_academic_terms(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_exam_rooms (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  exam_id BIGINT UNSIGNED NOT NULL,
  room_id BIGINT UNSIGNED NOT NULL,
  capacity_assigned INT UNSIGNED NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_exam_room (exam_id, room_id),
  CONSTRAINT fk_exam_room_exam
    FOREIGN KEY (exam_id) REFERENCES sms_exams(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_exam_room_room
    FOREIGN KEY (room_id) REFERENCES sms_rooms(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_exam_room_allocations (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  exam_id BIGINT UNSIGNED NOT NULL,
  room_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  seat_no VARCHAR(20) NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_exam_room_seat (exam_id, room_id, seat_no),
  UNIQUE KEY uq_exam_student (exam_id, student_id),
  CONSTRAINT fk_exam_alloc_exam
    FOREIGN KEY (exam_id) REFERENCES sms_exams(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_exam_alloc_room
    FOREIGN KEY (room_id) REFERENCES sms_rooms(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_exam_alloc_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_exam_invigilators (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  exam_id BIGINT UNSIGNED NOT NULL,
  teacher_id BIGINT UNSIGNED NOT NULL,
  room_id BIGINT UNSIGNED NULL,
  duty_date DATE NOT NULL,
  shift_name VARCHAR(50) NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_invigilator (exam_id, teacher_id, duty_date, shift_name),
  CONSTRAINT fk_invigilator_exam
    FOREIGN KEY (exam_id) REFERENCES sms_exams(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_invigilator_teacher
    FOREIGN KEY (teacher_id) REFERENCES sms_employees(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_invigilator_room
    FOREIGN KEY (room_id) REFERENCES sms_rooms(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_assessments (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  exam_id BIGINT UNSIGNED NOT NULL,
  class_subject_id BIGINT UNSIGNED NOT NULL,
  assessment_type ENUM('unit_test','assignment','project','practical','viva','written') NOT NULL,
  title VARCHAR(191) NOT NULL,
  max_marks DECIMAL(6,2) NOT NULL DEFAULT 100.00,
  weightage DECIMAL(5,2) NOT NULL DEFAULT 0.00,
  due_date DATE NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_assessment_exam
    FOREIGN KEY (exam_id) REFERENCES sms_exams(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_assessment_class_subject
    FOREIGN KEY (class_subject_id) REFERENCES sms_class_subjects(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_marks (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  assessment_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  marks_obtained DECIMAL(6,2) NOT NULL DEFAULT 0.00,
  grade_label VARCHAR(10) NULL,
  remarks VARCHAR(255) NULL,
  entered_by BIGINT UNSIGNED NULL,
  entered_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_marks (assessment_id, student_id),
  CONSTRAINT fk_marks_assessment
    FOREIGN KEY (assessment_id) REFERENCES sms_assessments(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_marks_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_marks_entered_by
    FOREIGN KEY (entered_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_exam_results (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  exam_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  total_marks DECIMAL(8,2) NOT NULL DEFAULT 0.00,
  percentage DECIMAL(6,2) NOT NULL DEFAULT 0.00,
  gpa DECIMAL(4,2) NOT NULL DEFAULT 0.00,
  cgpa DECIMAL(4,2) NOT NULL DEFAULT 0.00,
  rank_no INT UNSIGNED NULL,
  result_status ENUM('pass','fail','withheld') NOT NULL DEFAULT 'withheld',
  processed_at DATETIME NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_exam_result (exam_id, student_id),
  KEY idx_exam_result_status (result_status),
  CONSTRAINT fk_result_exam
    FOREIGN KEY (exam_id) REFERENCES sms_exams(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_result_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_report_card_templates (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  layout_json JSON NOT NULL,
  is_active TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_rc_template (branch_id, name),
  CONSTRAINT fk_rc_template_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_report_cards (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  exam_result_id BIGINT UNSIGNED NOT NULL,
  template_id BIGINT UNSIGNED NULL,
  pdf_path VARCHAR(255) NULL,
  shared_to_parent_at DATETIME NULL,
  status ENUM('generated','shared','archived') NOT NULL DEFAULT 'generated',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_report_card_result
    FOREIGN KEY (exam_result_id) REFERENCES sms_exam_results(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_report_card_template
    FOREIGN KEY (template_id) REFERENCES sms_report_card_templates(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- FEES / FINANCE / LEDGER
-- =========================

CREATE TABLE IF NOT EXISTS sms_fee_heads (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  code VARCHAR(50) NOT NULL,
  name VARCHAR(100) NOT NULL,
  fee_type ENUM('tuition','transport','hostel','exam','misc','library','fine','other') NOT NULL DEFAULT 'tuition',
  taxable TINYINT(1) NOT NULL DEFAULT 0,
  is_active TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_fee_head_code (branch_id, code),
  CONSTRAINT fk_fee_head_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_fee_structures (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  class_id BIGINT UNSIGNED NOT NULL,
  student_category VARCHAR(50) NULL,
  title VARCHAR(191) NOT NULL,
  due_day_of_month TINYINT UNSIGNED NOT NULL DEFAULT 10,
  late_fee_rule JSON NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_fee_structure (branch_id, academic_year_id, class_id, student_category, title),
  CONSTRAINT fk_fee_structure_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_fee_structure_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_fee_structure_class
    FOREIGN KEY (class_id) REFERENCES sms_classes(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_fee_structure_items (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  fee_structure_id BIGINT UNSIGNED NOT NULL,
  fee_head_id BIGINT UNSIGNED NOT NULL,
  amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  is_mandatory TINYINT(1) NOT NULL DEFAULT 1,
  is_recurring TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_fee_structure_item (fee_structure_id, fee_head_id),
  CONSTRAINT fk_fsi_structure
    FOREIGN KEY (fee_structure_id) REFERENCES sms_fee_structures(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_fsi_head
    FOREIGN KEY (fee_head_id) REFERENCES sms_fee_heads(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_student_fee_accounts (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  fee_structure_id BIGINT UNSIGNED NOT NULL,
  opening_balance DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  scholarship_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  concession_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  status ENUM('active','closed') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_student_fee_account (student_id, academic_year_id),
  CONSTRAINT fk_sfa_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_sfa_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_sfa_structure
    FOREIGN KEY (fee_structure_id) REFERENCES sms_fee_structures(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_installment_plans (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  fee_structure_id BIGINT UNSIGNED NOT NULL,
  installment_no INT UNSIGNED NOT NULL,
  due_date_rule ENUM('fixed_date','relative_month') NOT NULL DEFAULT 'fixed_date',
  due_date_value VARCHAR(50) NOT NULL,
  amount DECIMAL(12,2) NOT NULL,
  grace_days INT UNSIGNED NOT NULL DEFAULT 0,
  late_fee_type ENUM('flat','percent') NOT NULL DEFAULT 'flat',
  late_fee_value DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_installment (fee_structure_id, installment_no),
  CONSTRAINT fk_installment_structure
    FOREIGN KEY (fee_structure_id) REFERENCES sms_fee_structures(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_fee_invoices (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_fee_account_id BIGINT UNSIGNED NOT NULL,
  invoice_no VARCHAR(50) NOT NULL,
  issue_date DATE NOT NULL,
  due_date DATE NOT NULL,
  total_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  paid_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  outstanding_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  late_fee_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  status ENUM('draft','issued','partially_paid','paid','overdue','cancelled') NOT NULL DEFAULT 'issued',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_invoice_no (invoice_no),
  KEY idx_invoice_status (status),
  CONSTRAINT fk_invoice_account
    FOREIGN KEY (student_fee_account_id) REFERENCES sms_student_fee_accounts(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_fee_invoice_items (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  invoice_id BIGINT UNSIGNED NOT NULL,
  fee_head_id BIGINT UNSIGNED NOT NULL,
  amount DECIMAL(12,2) NOT NULL,
  discount_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  tax_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_fii_invoice
    FOREIGN KEY (invoice_id) REFERENCES sms_fee_invoices(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_fii_head
    FOREIGN KEY (fee_head_id) REFERENCES sms_fee_heads(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_fee_transactions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  transaction_no VARCHAR(50) NOT NULL,
  invoice_id BIGINT UNSIGNED NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  paid_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  amount DECIMAL(12,2) NOT NULL,
  payment_method ENUM('cash','cheque','upi','card','online','wallet') NOT NULL,
  gateway_name VARCHAR(50) NULL,
  gateway_ref VARCHAR(191) NULL,
  status ENUM('pending','success','failed','reversed','refunded') NOT NULL DEFAULT 'pending',
  received_by BIGINT UNSIGNED NULL,
  receipt_no VARCHAR(50) NULL,
  raw_response JSON NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_txn_no (transaction_no),
  UNIQUE KEY uq_receipt_no (receipt_no),
  KEY idx_txn_student (student_id),
  CONSTRAINT fk_txn_invoice
    FOREIGN KEY (invoice_id) REFERENCES sms_fee_invoices(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_txn_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_txn_received_by
    FOREIGN KEY (received_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_fee_payment_allocations (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  transaction_id BIGINT UNSIGNED NOT NULL,
  invoice_item_id BIGINT UNSIGNED NOT NULL,
  amount DECIMAL(12,2) NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_fpa_txn
    FOREIGN KEY (transaction_id) REFERENCES sms_fee_transactions(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_fpa_item
    FOREIGN KEY (invoice_item_id) REFERENCES sms_fee_invoice_items(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_scholarships (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  scholarship_type ENUM('merit','sports','staff','need_based','other') NOT NULL,
  amount_or_percent DECIMAL(12,2) NOT NULL,
  start_date DATE NOT NULL,
  end_date DATE NULL,
  approval_status ENUM('pending','approved','rejected') NOT NULL DEFAULT 'pending',
  approved_by BIGINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_scholarship_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_scholarship_approver
    FOREIGN KEY (approved_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_fee_concessions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  concession_type ENUM('sibling','staff','special','other') NOT NULL,
  amount_or_percent DECIMAL(12,2) NOT NULL,
  reason VARCHAR(255) NULL,
  approved_by BIGINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_concession_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_concession_approver
    FOREIGN KEY (approved_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_account_heads (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  parent_id BIGINT UNSIGNED NULL,
  code VARCHAR(50) NOT NULL,
  name VARCHAR(100) NOT NULL,
  type ENUM('asset','liability','income','expense','equity') NOT NULL,
  is_system TINYINT(1) NOT NULL DEFAULT 0,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_account_head_code (code),
  CONSTRAINT fk_account_parent
    FOREIGN KEY (parent_id) REFERENCES sms_account_heads(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_account_transactions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  txn_no VARCHAR(50) NOT NULL,
  txn_date DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  source_type VARCHAR(50) NOT NULL,
  source_id BIGINT UNSIGNED NOT NULL,
  description VARCHAR(255) NULL,
  status ENUM('draft','posted','reversed') NOT NULL DEFAULT 'posted',
  created_by BIGINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_account_txn_no (txn_no),
  CONSTRAINT fk_account_txn_user
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_account_transaction_lines (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  account_transaction_id BIGINT UNSIGNED NOT NULL,
  account_head_id BIGINT UNSIGNED NOT NULL,
  debit DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  credit DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  KEY idx_atl_txn (account_transaction_id),
  CONSTRAINT fk_atl_txn
    FOREIGN KEY (account_transaction_id) REFERENCES sms_account_transactions(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_atl_head
    FOREIGN KEY (account_head_id) REFERENCES sms_account_heads(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- TIMETABLE / SUBSTITUTION
-- =========================

CREATE TABLE IF NOT EXISTS sms_timetable_templates (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  class_id BIGINT UNSIGNED NOT NULL,
  section_id BIGINT UNSIGNED NULL,
  title VARCHAR(191) NOT NULL,
  status ENUM('draft','published','archived') NOT NULL DEFAULT 'draft',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_tt_template_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_tt_template_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_tt_template_class
    FOREIGN KEY (class_id) REFERENCES sms_classes(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_tt_template_section
    FOREIGN KEY (section_id) REFERENCES sms_sections(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_timetable_slots (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  template_id BIGINT UNSIGNED NOT NULL,
  day_of_week TINYINT UNSIGNED NOT NULL,
  period_no INT UNSIGNED NOT NULL,
  start_time TIME NOT NULL,
  end_time TIME NOT NULL,
  subject_id BIGINT UNSIGNED NOT NULL,
  teacher_id BIGINT UNSIGNED NULL,
  room_id BIGINT UNSIGNED NULL,
  is_fixed TINYINT(1) NOT NULL DEFAULT 0,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_timetable_slot (template_id, day_of_week, period_no),
  CONSTRAINT fk_slot_template
    FOREIGN KEY (template_id) REFERENCES sms_timetable_templates(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_slot_subject
    FOREIGN KEY (subject_id) REFERENCES sms_subjects(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_slot_teacher
    FOREIGN KEY (teacher_id) REFERENCES sms_employees(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_slot_room
    FOREIGN KEY (room_id) REFERENCES sms_rooms(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_teacher_substitutions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  timetable_slot_id BIGINT UNSIGNED NOT NULL,
  original_teacher_id BIGINT UNSIGNED NOT NULL,
  substitute_teacher_id BIGINT UNSIGNED NOT NULL,
  substitution_date DATE NOT NULL,
  reason VARCHAR(255) NULL,
  approved_by BIGINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_substitution (timetable_slot_id, substitution_date),
  CONSTRAINT fk_sub_slot
    FOREIGN KEY (timetable_slot_id) REFERENCES sms_timetable_slots(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_sub_original
    FOREIGN KEY (original_teacher_id) REFERENCES sms_employees(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_substitute_teacher
    FOREIGN KEY (substitute_teacher_id) REFERENCES sms_employees(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_sub_approved_by
    FOREIGN KEY (approved_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_class_teachers (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  class_id BIGINT UNSIGNED NOT NULL,
  section_id BIGINT UNSIGNED NULL,
  teacher_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  is_primary TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_class_teacher (class_id, section_id, teacher_id, academic_year_id),
  CONSTRAINT fk_ct_class
    FOREIGN KEY (class_id) REFERENCES sms_classes(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_ct_section
    FOREIGN KEY (section_id) REFERENCES sms_sections(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_ct_teacher
    FOREIGN KEY (teacher_id) REFERENCES sms_employees(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_ct_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- HOMEWORK / ASSIGNMENTS / LMS
-- =========================

CREATE TABLE IF NOT EXISTS sms_homeworks (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  class_subject_id BIGINT UNSIGNED NOT NULL,
  assigned_by BIGINT UNSIGNED NOT NULL,
  title VARCHAR(191) NOT NULL,
  description TEXT NULL,
  due_date DATE NOT NULL,
  attachment_path VARCHAR(255) NULL,
  status ENUM('draft','published','closed') NOT NULL DEFAULT 'published',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  CONSTRAINT fk_hw_class_subject
    FOREIGN KEY (class_subject_id) REFERENCES sms_class_subjects(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_hw_assigned_by
    FOREIGN KEY (assigned_by) REFERENCES sms_users(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_homework_submissions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  homework_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  submitted_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  content_text TEXT NULL,
  attachment_path VARCHAR(255) NULL,
  score DECIMAL(6,2) NULL,
  feedback TEXT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_hw_submission (homework_id, student_id),
  CONSTRAINT fk_hwsub_homework
    FOREIGN KEY (homework_id) REFERENCES sms_homeworks(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_hwsub_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_assignments (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  class_subject_id BIGINT UNSIGNED NOT NULL,
  title VARCHAR(191) NOT NULL,
  instructions TEXT NULL,
  due_date DATE NOT NULL,
  max_marks DECIMAL(6,2) NOT NULL DEFAULT 100.00,
  attachment_path VARCHAR(255) NULL,
  created_by BIGINT UNSIGNED NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_assignment_class_subject
    FOREIGN KEY (class_subject_id) REFERENCES sms_class_subjects(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_assignment_creator
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_assignment_submissions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  assignment_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  submitted_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  file_path VARCHAR(255) NULL,
  marks DECIMAL(6,2) NULL,
  feedback TEXT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_assignment_submission (assignment_id, student_id),
  CONSTRAINT fk_asn_assignment
    FOREIGN KEY (assignment_id) REFERENCES sms_assignments(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_asn_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_projects (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  class_subject_id BIGINT UNSIGNED NOT NULL,
  project_type ENUM('group','individual') NOT NULL DEFAULT 'individual',
  title VARCHAR(191) NOT NULL,
  description TEXT NULL,
  due_date DATE NOT NULL,
  created_by BIGINT UNSIGNED NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_project_class_subject
    FOREIGN KEY (class_subject_id) REFERENCES sms_class_subjects(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_project_creator
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_project_members (
  project_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  role_in_project VARCHAR(100) NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (project_id, student_id),
  CONSTRAINT fk_pm_project
    FOREIGN KEY (project_id) REFERENCES sms_projects(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_pm_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_lms_content (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  class_id BIGINT UNSIGNED NULL,
  subject_id BIGINT UNSIGNED NULL,
  title VARCHAR(191) NOT NULL,
  content_type ENUM('video','document','pdf','presentation','link','quiz') NOT NULL,
  file_path VARCHAR(255) NULL,
  url VARCHAR(255) NULL,
  description TEXT NULL,
  visibility ENUM('teachers','students','parents','all') NOT NULL DEFAULT 'students',
  created_by BIGINT UNSIGNED NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_lms_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_lms_class
    FOREIGN KEY (class_id) REFERENCES sms_classes(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_lms_subject
    FOREIGN KEY (subject_id) REFERENCES sms_subjects(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_lms_creator
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_online_classes (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  class_subject_id BIGINT UNSIGNED NOT NULL,
  platform ENUM('zoom','meet','teams','other') NOT NULL,
  meeting_url VARCHAR(255) NOT NULL,
  meeting_id VARCHAR(100) NULL,
  passcode VARCHAR(100) NULL,
  start_at DATETIME NOT NULL,
  end_at DATETIME NOT NULL,
  created_by BIGINT UNSIGNED NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_online_class_subject
    FOREIGN KEY (class_subject_id) REFERENCES sms_class_subjects(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_online_class_creator
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_quizzes (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  class_subject_id BIGINT UNSIGNED NOT NULL,
  title VARCHAR(191) NOT NULL,
  instructions TEXT NULL,
  max_attempts INT UNSIGNED NOT NULL DEFAULT 1,
  time_limit_minutes INT UNSIGNED NULL,
  status ENUM('draft','published','closed') NOT NULL DEFAULT 'draft',
  created_by BIGINT UNSIGNED NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_quiz_class_subject
    FOREIGN KEY (class_subject_id) REFERENCES sms_class_subjects(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_quiz_creator
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_quiz_questions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  quiz_id BIGINT UNSIGNED NOT NULL,
  question_type ENUM('mcq','true_false','short_answer','long_answer') NOT NULL DEFAULT 'mcq',
  question_text TEXT NOT NULL,
  options_json JSON NULL,
  correct_answer TEXT NULL,
  marks DECIMAL(6,2) NOT NULL DEFAULT 1.00,
  sort_order INT NOT NULL DEFAULT 0,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_quiz_q_quiz
    FOREIGN KEY (quiz_id) REFERENCES sms_quizzes(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_quiz_attempts (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  quiz_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  started_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  submitted_at DATETIME NULL,
  score DECIMAL(6,2) NULL,
  status ENUM('started','submitted','graded') NOT NULL DEFAULT 'started',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_quiz_attempt (quiz_id, student_id, started_at),
  CONSTRAINT fk_quiz_attempt_quiz
    FOREIGN KEY (quiz_id) REFERENCES sms_quizzes(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_quiz_attempt_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- COMMUNICATION
-- =========================

CREATE TABLE IF NOT EXISTS sms_message_templates (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  channel ENUM('sms','email','push','whatsapp') NOT NULL,
  template_key VARCHAR(100) NOT NULL,
  subject VARCHAR(191) NULL,
  body ტექస్ట్ NULL,
  variables_json JSON NULL,
  is_active TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  UNIQUE KEY uq_template_key (channel, template_key)
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_notifications (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  recipient_user_id BIGINT UNSIGNED NULL,
  channel ENUM('sms','email','push','whatsapp') NOT NULL,
  template_key VARCHAR(100) NOT NULL,
  payload_json JSON NOT NULL,
  status ENUM('queued','sent','delivered','failed') NOT NULL DEFAULT 'queued',
  scheduled_at DATETIME NULL,
  sent_at DATETIME NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  KEY idx_notification_recipient (recipient_user_id),
  CONSTRAINT fk_notification_user
    FOREIGN KEY (recipient_user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_message_logs (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  notification_id BIGINT UNSIGNED NULL,
  provider_name VARCHAR(100) NOT NULL,
  provider_message_id VARCHAR(191) NULL,
  status ENUM('queued','sent','delivered','failed') NOT NULL,
  error_message VARCHAR(255) NULL,
  sent_at DATETIME NULL,
  delivered_at DATETIME NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_msg_log_notification
    FOREIGN KEY (notification_id) REFERENCES sms_notifications(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_circulars (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  title VARCHAR(191) NOT NULL,
  content TEXT NOT NULL,
  audience_scope ENUM('all','students','parents','staff','teachers') NOT NULL DEFAULT 'all',
  publish_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  expiry_at DATETIME NULL,
  attachment_path VARCHAR(255) NULL,
  created_by BIGINT UNSIGNED NULL,
  status ENUM('draft','published','archived') NOT NULL DEFAULT 'published',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_circular_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_circular_creator
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_announcements (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  title VARCHAR(191) NOT NULL,
  content TEXT NOT NULL,
  audience_scope ENUM('all','students','parents','staff','teachers') NOT NULL DEFAULT 'all',
  priority ENUM('low','normal','high','critical') NOT NULL DEFAULT 'normal',
  is_emergency TINYINT(1) NOT NULL DEFAULT 0,
  publish_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  created_by BIGINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_announcement_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_announcement_creator
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- TRANSPORT
-- =========================

CREATE TABLE IF NOT EXISTS sms_transport_vehicles (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  registration_no VARCHAR(50) NOT NULL,
  vehicle_no VARCHAR(50) NULL,
  model VARCHAR(100) NULL,
  capacity INT UNSIGNED NOT NULL DEFAULT 0,
  fuel_type VARCHAR(50) NULL,
  insurance_expiry DATE NULL,
  fitness_expiry DATE NULL,
  status ENUM('active','inactive','maintenance') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_vehicle_reg (registration_no),
  CONSTRAINT fk_vehicle_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_transport_routes (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  route_code VARCHAR(50) NOT NULL,
  name VARCHAR(100) NOT NULL,
  start_point VARCHAR(191) NULL,
  end_point VARCHAR(191) NULL,
  total_distance_km DECIMAL(8,2) NULL,
  active TINYINT(1) NOT NULL DEFAULT 1,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_route_code (branch_id, route_code),
  CONSTRAINT fk_route_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_transport_route_stops (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  route_id BIGINT UNSIGNED NOT NULL,
  stop_name VARCHAR(191) NOT NULL,
  stop_order INT NOT NULL,
  latitude DECIMAL(10,7) NULL,
  longitude DECIMAL(10,7) NULL,
  estimated_time TIME NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_route_stop (route_id, stop_order),
  CONSTRAINT fk_route_stop_route
    FOREIGN KEY (route_id) REFERENCES sms_transport_routes(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_student_transport_assignments (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  route_id BIGINT UNSIGNED NOT NULL,
  stop_id BIGINT UNSIGNED NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  pickup_bus_no VARCHAR(50) NULL,
  drop_bus_no VARCHAR(50) NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_student_transport (student_id, academic_year_id),
  CONSTRAINT fk_sta_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_sta_route
    FOREIGN KEY (route_id) REFERENCES sms_transport_routes(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_sta_stop
    FOREIGN KEY (stop_id) REFERENCES sms_transport_route_stops(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_sta_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_gps_tracks (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  vehicle_id BIGINT UNSIGNED NOT NULL,
  tracked_at DATETIME NOT NULL,
  latitude DECIMAL(10,7) NOT NULL,
  longitude DECIMAL(10,7) NOT NULL,
  speed DECIMAL(8,2) NULL,
  ignition_status ENUM('on','off') NULL,
  source VARCHAR(50) NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  KEY idx_gps_vehicle_time (vehicle_id, tracked_at),
  CONSTRAINT fk_gps_vehicle
    FOREIGN KEY (vehicle_id) REFERENCES sms_transport_vehicles(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- HOSTEL
-- =========================

CREATE TABLE IF NOT EXISTS sms_hostels (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  gender_type ENUM('male','female','coed') NOT NULL DEFAULT 'coed',
  warden_user_id BIGINT UNSIGNED NULL,
  capacity INT UNSIGNED NOT NULL DEFAULT 0,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_hostel (branch_id, name),
  CONSTRAINT fk_hostel_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_hostel_warden
    FOREIGN KEY (warden_user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_hostel_rooms (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  hostel_id BIGINT UNSIGNED NOT NULL,
  room_no VARCHAR(50) NOT NULL,
  floor_no INT NULL,
  capacity INT UNSIGNED NOT NULL DEFAULT 4,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_hostel_room (hostel_id, room_no),
  CONSTRAINT fk_hostel_room_hostel
    FOREIGN KEY (hostel_id) REFERENCES sms_hostels(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_hostel_beds (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  room_id BIGINT UNSIGNED NOT NULL,
  bed_no VARCHAR(50) NOT NULL,
  status ENUM('available','allocated','maintenance') NOT NULL DEFAULT 'available',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_bed (room_id, bed_no),
  CONSTRAINT fk_bed_room
    FOREIGN KEY (room_id) REFERENCES sms_hostel_rooms(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_hostel_allocations (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  bed_id BIGINT UNSIGNED NOT NULL,
  academic_year_id BIGINT UNSIGNED NOT NULL,
  check_in_date DATE NOT NULL,
  check_out_date DATE NULL,
  status ENUM('active','inactive','checked_out') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_hostel_alloc (student_id, academic_year_id),
  CONSTRAINT fk_halloc_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_halloc_bed
    FOREIGN KEY (bed_id) REFERENCES sms_hostel_beds(id)
    ON DELETE RESTRICT ON UPDATE CASCADE,
  CONSTRAINT fk_halloc_year
    FOREIGN KEY (academic_year_id) REFERENCES sms_academic_years(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_hostel_attendance (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  hostel_allocation_id BIGINT UNSIGNED NOT NULL,
  attendance_date DATE NOT NULL,
  check_in_at DATETIME NULL,
  check_out_at DATETIME NULL,
  status ENUM('present','absent','leave') NOT NULL DEFAULT 'present',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_hostel_att (hostel_allocation_id, attendance_date),
  CONSTRAINT fk_hostel_att_alloc
    FOREIGN KEY (hostel_allocation_id) REFERENCES sms_hostel_allocations(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_hostel_bills (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  month_year CHAR(7) NOT NULL,
  hostel_fee DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  mess_fee DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  other_charges DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  total_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  due_date DATE NOT NULL,
  status ENUM('draft','issued','paid','overdue','cancelled') NOT NULL DEFAULT 'issued',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_hostel_bill (student_id, month_year),
  CONSTRAINT fk_hostel_bill_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- LIBRARY
-- =========================

CREATE TABLE IF NOT EXISTS sms_library_items (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  item_type ENUM('book','journal','magazine','ebook') NOT NULL,
  title VARCHAR(191) NOT NULL,
  author VARCHAR(191) NULL,
  publisher VARCHAR(191) NULL,
  isbn VARCHAR(30) NULL,
  category VARCHAR(100) NULL,
  subject_id BIGINT UNSIGNED NULL,
  total_copies INT UNSIGNED NOT NULL DEFAULT 0,
  available_copies INT UNSIGNED NOT NULL DEFAULT 0,
  shelf_no VARCHAR(50) NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  KEY idx_lib_title (title),
  CONSTRAINT fk_library_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_library_subject
    FOREIGN KEY (subject_id) REFERENCES sms_subjects(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_library_copies (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  library_item_id BIGINT UNSIGNED NOT NULL,
  accession_no VARCHAR(50) NOT NULL,
  barcode VARCHAR(100) NULL,
  status ENUM('available','issued','reserved','lost','damaged') NOT NULL DEFAULT 'available',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_accession (accession_no),
  UNIQUE KEY uq_barcode (barcode),
  CONSTRAINT fk_copy_item
    FOREIGN KEY (library_item_id) REFERENCES sms_library_items(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_library_loans (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  copy_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NULL,
  staff_id BIGINT UNSIGNED NULL,
  issued_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  due_at DATETIME NOT NULL,
  returned_at DATETIME NULL,
  fine_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  status ENUM('issued','returned','overdue','lost') NOT NULL DEFAULT 'issued',
  CONSTRAINT fk_loan_copy
    FOREIGN KEY (copy_id) REFERENCES sms_library_copies(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_loan_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_loan_staff
    FOREIGN KEY (staff_id) REFERENCES sms_employees(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_library_reservations (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  library_item_id BIGINT UNSIGNED NOT NULL,
  user_id BIGINT UNSIGNED NOT NULL,
  reserved_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  status ENUM('active','fulfilled','cancelled','expired') NOT NULL DEFAULT 'active',
  CONSTRAINT fk_reservation_item
    FOREIGN KEY (library_item_id) REFERENCES sms_library_items(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_reservation_user
    FOREIGN KEY (user_id) REFERENCES sms_users(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- INVENTORY / ASSETS / PROCUREMENT
-- =========================

CREATE TABLE IF NOT EXISTS sms_vendors (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(191) NOT NULL,
  contact_person VARCHAR(191) NULL,
  phone VARCHAR(30) NULL,
  email VARCHAR(191) NULL,
  address TEXT NULL,
  tax_no VARCHAR(50) NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_vendor_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_inventory_items (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  item_code VARCHAR(50) NOT NULL,
  name VARCHAR(191) NOT NULL,
  category VARCHAR(100) NOT NULL,
  unit VARCHAR(30) NOT NULL DEFAULT 'pcs',
  min_stock INT UNSIGNED NOT NULL DEFAULT 0,
  current_stock INT UNSIGNED NOT NULL DEFAULT 0,
  reorder_level INT UNSIGNED NOT NULL DEFAULT 0,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_inventory_code (branch_id, item_code),
  CONSTRAINT fk_inventory_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_purchase_orders (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  vendor_id BIGINT UNSIGNED NOT NULL,
  po_no VARCHAR(50) NOT NULL,
  order_date DATE NOT NULL,
  expected_date DATE NULL,
  status ENUM('draft','sent','partial','received','cancelled') NOT NULL DEFAULT 'draft',
  total_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_po_no (po_no),
  CONSTRAINT fk_po_vendor
    FOREIGN KEY (vendor_id) REFERENCES sms_vendors(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_purchase_order_items (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  purchase_order_id BIGINT UNSIGNED NOT NULL,
  inventory_item_id BIGINT UNSIGNED NOT NULL,
  qty DECIMAL(12,2) NOT NULL,
  unit_price DECIMAL(12,2) NOT NULL,
  total DECIMAL(12,2) NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_poi_po
    FOREIGN KEY (purchase_order_id) REFERENCES sms_purchase_orders(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_poi_item
    FOREIGN KEY (inventory_item_id) REFERENCES sms_inventory_items(id)
    ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_stock_movements (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  inventory_item_id BIGINT UNSIGNED NOT NULL,
  movement_type ENUM('in','out','adjustment') NOT NULL,
  qty DECIMAL(12,2) NOT NULL,
  ref_type VARCHAR(50) NULL,
  ref_id BIGINT UNSIGNED NULL,
  note VARCHAR(255) NULL,
  moved_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_stock_item
    FOREIGN KEY (inventory_item_id) REFERENCES sms_inventory_items(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_assets (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  asset_code VARCHAR(50) NOT NULL,
  asset_name VARCHAR(191) NOT NULL,
  category VARCHAR(100) NOT NULL,
  purchase_date DATE NULL,
  purchase_price DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  useful_life_months INT UNSIGNED NULL,
  status ENUM('active','inactive','disposed') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_asset_code (asset_code),
  CONSTRAINT fk_asset_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_asset_assignments (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  asset_id BIGINT UNSIGNED NOT NULL,
  assigned_to_user_id BIGINT UNSIGNED NULL,
  assigned_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  returned_at DATETIME NULL,
  condition_note VARCHAR(255) NULL,
  CONSTRAINT fk_asset_assign_asset
    FOREIGN KEY (asset_id) REFERENCES sms_assets(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_asset_assign_user
    FOREIGN KEY (assigned_to_user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_asset_maintenance (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  asset_id BIGINT UNSIGNED NOT NULL,
  maintenance_date DATE NOT NULL,
  cost DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  description TEXT NULL,
  status ENUM('planned','done','cancelled') NOT NULL DEFAULT 'planned',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_asset_maint_asset
    FOREIGN KEY (asset_id) REFERENCES sms_assets(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_asset_depreciation (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  asset_id BIGINT UNSIGNED NOT NULL,
  period_year SMALLINT UNSIGNED NOT NULL,
  period_month TINYINT UNSIGNED NOT NULL,
  depreciation_amount DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_asset_dep (asset_id, period_year, period_month),
  CONSTRAINT fk_asset_dep_asset
    FOREIGN KEY (asset_id) REFERENCES sms_assets(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

-- =========================
-- EVENTS / DISCIPLINE / ALUMNI
-- =========================

CREATE TABLE IF NOT EXISTS sms_events (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  event_type VARCHAR(50) NOT NULL,
  title VARCHAR(191) NOT NULL,
  description TEXT NULL,
  start_at DATETIME NOT NULL,
  end_at DATETIME NOT NULL,
  venue VARCHAR(191) NULL,
  budget DECIMAL(12,2) NOT NULL DEFAULT 0.00,
  status ENUM('draft','published','ongoing','completed','cancelled') NOT NULL DEFAULT 'draft',
  created_by BIGINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_event_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_event_creator
    FOREIGN KEY (created_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_event_registrations (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  event_id BIGINT UNSIGNED NOT NULL,
  user_id BIGINT UNSIGNED NULL,
  student_id BIGINT UNSIGNED NULL,
  participation_role VARCHAR(100) NULL,
  status ENUM('registered','attended','absent','cancelled') NOT NULL DEFAULT 'registered',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_event_reg_event
    FOREIGN KEY (event_id) REFERENCES sms_events(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_event_reg_user
    FOREIGN KEY (user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_event_reg_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_certificates (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  certificate_no VARCHAR(50) NOT NULL,
  certificate_type VARCHAR(100) NOT NULL,
  entity_type VARCHAR(100) NOT NULL,
  entity_id BIGINT UNSIGNED NOT NULL,
  issued_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  file_path VARCHAR(255) NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_certificate_no (certificate_no)
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_discipline_incidents (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  reported_by BIGINT UNSIGNED NULL,
  incident_date DATE NOT NULL,
  category VARCHAR(100) NOT NULL,
  severity ENUM('low','medium','high','critical') NOT NULL DEFAULT 'low',
  description TEXT NOT NULL,
  status ENUM('open','under_review','resolved','closed') NOT NULL DEFAULT 'open',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_incident_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_incident_reporter
    FOREIGN KEY (reported_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_discipline_actions (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  incident_id BIGINT UNSIGNED NOT NULL,
  action_type ENUM('warning','counseling','suspension','community_service','parent_meeting','other') NOT NULL,
  action_date DATE NOT NULL,
  details TEXT NULL,
  decided_by BIGINT UNSIGNED NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_action_incident
    FOREIGN KEY (incident_id) REFERENCES sms_discipline_incidents(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_action_decided_by
    FOREIGN KEY (decided_by) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_behavior_scores (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  student_id BIGINT UNSIGNED NOT NULL,
  period_start DATE NOT NULL,
  period_end DATE NOT NULL,
  score DECIMAL(6,2) NOT NULL DEFAULT 0.00,
  remarks TEXT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_behavior_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_alumni_profiles (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  user_id BIGINT UNSIGNED NULL,
  student_id BIGINT UNSIGNED NULL,
  passing_year SMALLINT UNSIGNED NULL,
  current_job VARCHAR(191) NULL,
  company VARCHAR(191) NULL,
  city VARCHAR(100) NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  KEY idx_alumni_user (user_id),
  CONSTRAINT fk_alumni_user
    FOREIGN KEY (user_id) REFERENCES sms_users(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_alumni_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_alumni_groups (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  branch_id BIGINT UNSIGNED NOT NULL,
  name VARCHAR(100) NOT NULL,
  description TEXT NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  UNIQUE KEY uq_alumni_group (branch_id, name),
  CONSTRAINT fk_alumni_group_branch
    FOREIGN KEY (branch_id) REFERENCES sms_branches(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_alumni_group_members (
  group_id BIGINT UNSIGNED NOT NULL,
  alumni_profile_id BIGINT UNSIGNED NOT NULL,
  joined_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  PRIMARY KEY (group_id, alumni_profile_id),
  CONSTRAINT fk_agm_group
    FOREIGN KEY (group_id) REFERENCES sms_alumni_groups(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_agm_profile
    FOREIGN KEY (alumni_profile_id) REFERENCES sms_alumni_profiles(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_donations (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  alumni_profile_id BIGINT UNSIGNED NULL,
  event_id BIGINT UNSIGNED NULL,
  amount DECIMAL(12,2) NOT NULL,
  donated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  purpose VARCHAR(191) NULL,
  payment_status ENUM('pending','success','failed') NOT NULL DEFAULT 'pending',
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_donation_alumni
    FOREIGN KEY (alumni_profile_id) REFERENCES sms_alumni_profiles(id)
    ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT fk_donation_event
    FOREIGN KEY (event_id) REFERENCES sms_events(id)
    ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS sms_mentorships (
  id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  alumni_profile_id BIGINT UNSIGNED NOT NULL,
  student_id BIGINT UNSIGNED NOT NULL,
  start_date DATE NOT NULL,
  end_date DATE NULL,
  status ENUM('active','inactive') NOT NULL DEFAULT 'active',
  notes TEXT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_mentorship_alumni
    FOREIGN KEY (alumni_profile_id) REFERENCES sms_alumni_profiles(id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT fk_mentorship_student
    FOREIGN KEY (student_id) REFERENCES sms_students(id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

SET FOREIGN_KEY_CHECKS = 1;
```

## 2) ERD DESCRIPTION

`sms_institutions 1---* sms_branches`
`sms_branches 1---* sms_academic_years`
`sms_academic_years 1---* sms_academic_terms`
`sms_branches 1---* sms_classes`
`sms_classes 1---* sms_sections`
`sms_classes 1---* sms_class_subjects`
`sms_subjects 1---* sms_class_subjects`
`sms_users 1---* sms_user_roles` and `sms_roles 1---* sms_user_roles`
`sms_roles 1---* sms_role_permissions` and `sms_permissions 1---* sms_role_permissions`
`sms_users 1---* sms_audit_logs`
`sms_users 1---* sms_employees` via `user_id`
`sms_users 1---* sms_students` via `user_id`
`sms_students *---* sms_guardians` through `sms_student_guardians`
`sms_students 1---* sms_student_documents`
`sms_students 1---* sms_student_lifecycle_events`
`sms_students 1---* sms_student_attendance`
`sms_attendance_sessions 1---* sms_student_attendance`
`sms_employees 1---* sms_staff_attendance`
`sms_exam_types 1---* sms_exams`
`sms_exams 1---* sms_assessments`
`sms_assessments 1---* sms_marks`
`sms_exams 1---* sms_exam_results`
`sms_exam_results 1---1 sms_report_cards`
`sms_students 1---* sms_student_fee_accounts`
`sms_student_fee_accounts 1---* sms_fee_invoices`
`sms_fee_invoices 1---* sms_fee_invoice_items`
`sms_fee_invoices 1---* sms_fee_transactions`
`sms_fee_transactions 1---* sms_fee_payment_allocations`
`sms_account_transactions 1---* sms_account_transaction_lines`
`sms_timetable_templates 1---* sms_timetable_slots`
`sms_timetable_slots 1---* sms_teacher_substitutions`
`sms_class_subjects 1---* sms_homeworks` / `sms_assignments` / `sms_projects` / `sms_online_classes` / `sms_quizzes`
`sms_quizzes 1---* sms_quiz_questions` and `sms_quiz_attempts`
`sms_transport_routes 1---* sms_transport_route_stops`
`sms_transport_routes 1---* sms_student_transport_assignments`
`sms_transport_vehicles 1---* sms_gps_tracks`
`sms_hostels 1---* sms_hostel_rooms 1---* sms_hostel_beds 1---* sms_hostel_allocations 1---* sms_hostel_attendance`
`sms_library_items 1---* sms_library_copies 1---* sms_library_loans`
`sms_inventory_items 1---* sms_purchase_order_items` and `sms_stock_movements`
`sms_assets 1---* sms_asset_assignments` / `sms_asset_maintenance` / `sms_asset_depreciation`
`sms_students 1---* sms_discipline_incidents`
`sms_students 1---* sms_behavior_scores`
`sms_alumni_profiles 1---* sms_alumni_group_members`
`sms_alumni_profiles 1---* sms_donations`
`sms_alumni_profiles 1---* sms_mentorships`

Critical relationships:

* A student belongs to exactly one current branch/class/academic year and optionally a section, house, hostel bed, and transport assignment.
* Fee collection links to student fee accounts, invoices, and line-level allocations; those allocations drive receipt, due, and ledger state.
* Timetable slots determine teacher and room availability; substitutions override a slot for a date.
* Exams produce assessments, marks, results, and report cards; results can be blocked by attendance or fee policy.
* Admissions create the student, guardian, user account, documents, and lifecycle event in one atomic workflow.

## 3) PHP PROJECT STRUCTURE (Plain PHP MVC)

```text
sms/
├── public/
│   ├── index.php
│   ├── .htaccess
│   ├── assets/
│   └── uploads/
├── app/
│   ├── Core/
│   │   ├── Database.php
│   │   ├── Model.php
│   │   ├── Controller.php
│   │   ├── Router.php
│   │   ├── Auth.php
│   │   ├── Rbac.php
│   │   ├── Csrf.php
│   │   ├── Validator.php
│   │   ├── Logger.php
│   │   ├── Pdf.php
│   │   └── Response.php
│   ├── Middleware/
│   │   ├── Authenticate.php
│   │   └── Permission.php
│   ├── Helpers/
│   │   ├── functions.php
│   │   ├── format.php
│   │   └── upload.php
│   ├── Config/
│   │   ├── app.php
│   │   ├── database.php
│   │   ├── mail.php
│   │   ├── sms.php
│   │   └── constants.php
│   ├── Services/
│   │   ├── SmsService.php
│   │   ├── MailService.php
│   │   ├── FeeService.php
│   │   ├── ResultService.php
│   │   └── TimetableService.php
│   └── Views/
│       ├── layouts/
│       └── errors/
├── modules/
│   ├── auth/
│   ├── dashboard/
│   ├── master/
│   ├── admission/
│   ├── student/
│   ├── parent/
│   ├── academic/
│   ├── attendance/
│   ├── exam/
│   ├── fee/
│   ├── timetable/
│   ├── homework/
│   ├── lms/
│   ├── communication/
│   ├── transport/
│   ├── hostel/
│   ├── library/
│   ├── inventory/
│   ├── hrms/
│   ├── events/
│   ├── discipline/
│   └── alumni/
├── routes/
│   ├── web.php
│   └── api.php
├── storage/
│   ├── logs/
│   ├── cache/
│   └── exports/
├── vendor/
├── composer.json
└── .env
```

`.htaccess`:

```apache
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^ index.php [QSA,L]
```

Composer packages:

* `phpmailer/phpmailer`
* `dompdf/dompdf`
* `phpoffice/phpspreadsheet`
* `vlucas/phpdotenv`

## 4) CROSS-MODULE INTERACTION & BUSINESS LOGIC

### Admissions

Trigger: approved application
Data flow: `sms_admission_applications` → `sms_students` → `sms_guardians` → `sms_student_guardians` → `sms_users` → `sms_student_documents` → `sms_student_lifecycle_events`
Validation:

* class capacity not exceeded
* documents present
* duplicate admission no not allowed
* age/class rule satisfied
  Edge cases:
* if user creation fails, rollback everything
* if roll number collision occurs, regenerate inside transaction
  Concurrency:
* use row locking on admission sequence source or a unique index on `(branch_id, academic_year_id, roll_no)`

### Attendance → Exam eligibility

Trigger: attendance finalized
Data flow: `sms_student_attendance` aggregated by student/term
Validation:

* minimum attendance percentage configured per branch/class
* late/excused rules applied separately
  Edge cases:
* leave applications can mark a day excused
* biometric sync retries must be idempotent
  Concurrency:
* attendance session locked before finalization

### Fee collection → Exam/report card release

Trigger: successful fee transaction
Data flow: `sms_fee_transactions` → update `sms_fee_invoices` → post `sms_account_transactions`/lines
Validation:

* invoice must be open
* payment amount cannot exceed outstanding unless overpayment policy allows credit
  Edge cases:
* duplicate gateway callback ignored via `gateway_ref` unique check
* partial payment updates invoice to `partially_paid`
  Concurrency:
* wrap invoice update + transaction insert + ledger posting in a single DB transaction with `SELECT ... FOR UPDATE`

### Timetable → Teacher substitution

Trigger: teacher absence or admin override
Data flow: `sms_timetable_slots` → `sms_teacher_substitutions`
Validation:

* substitute must not clash on the same date/period
* room capacity and teacher availability must still be valid
  Edge cases:
* if slot was already substituted, block duplicate override
  Concurrency:
* unique key on `(timetable_slot_id, substitution_date)` prevents double substitution

### Exam → Result processing

Trigger: marks entry closed
Data flow: `sms_marks` → `sms_exam_results` → `sms_report_cards`
Validation:

* all assessments complete
* no missing mandatory marks
* grade scale exists
  Edge cases:
* withheld result when any mandatory component is missing
* recheck/revaluation updates result version, not overwrites history

### Transport / Hostel / Library / HRMS

* Transport assignment can be used to charge transport fee head automatically.
* Hostel allocation can generate hostel fee bills and attendance eligibility.
* Library overdue fines can post into `sms_fee_transactions` as fine fee head.
* HRMS leave and staff attendance can affect payroll if added later.

## 5) CRITICAL ALGORITHMS

### Grading & GPA

1. Sum weighted marks per subject.
2. Convert percentage to grade using `sms_grade_scales`.
3. Grade points use the matching scale.
4. GPA = weighted average of grade points by credit hours.
5. CGPA = average of term GPAs or weighted by credits if you want academic rigor.

### Student promotion

Rules:

* all fee and disciplinary blocks cleared
* attendance threshold met
* exam result computed
* if failed in core subjects, mark repeat/back-paper
  Process:
* create `sms_student_lifecycle_events`
* update `sms_students.current_class_id/current_section_id/academic_year_id`
* preserve previous class/year in lifecycle history

### Fee installment and late fee

* due date comes from fee structure or installment plan.
* grace days apply after due date.
* late fee can be flat or percentage per day/week/month.
* overdue invoices are re-computed by service, not by manual edit.

### Timetable auto-scheduling

Use constraint solving:

* teacher availability
* room capacity
* subject period requirements
* lab subjects require lab rooms
* avoid teacher/room clashes
  Practical approach:
* greedy assignment by hardest constraints first
* fallback to backtracking on conflicts
* if no fit, mark unresolved slot for admin review

### Attendance analytics

* class attendance % = present sessions / total sessions
* student default list = below threshold or repeated absences
* exam eligibility can query thresholds by class or branch settings

## 6) API / SERVICE CONTRACTS

Auth:

* `POST /api/v1/auth/login`
* `POST /api/v1/auth/logout`
* `POST /api/v1/auth/forgot-password`
* `POST /api/v1/auth/reset-password`

Student/admission:

* `GET /api/v1/admissions/applications`
* `POST /api/v1/admissions/applications`
* `POST /api/v1/admissions/applications/{id}/approve`
* `POST /api/v1/students`
* `GET /api/v1/students/{id}`

Attendance:

* `POST /api/v1/attendance/student/bulk-mark`
* `POST /api/v1/attendance/staff/bulk-mark`
* `GET /api/v1/attendance/analytics/{class_id}`

Fees:

* `POST /api/v1/fees/invoices`
* `POST /api/v1/fees/collect`
* `GET /api/v1/fees/student/{id}/ledger`
* `POST /api/v1/fees/refund`

Exams:

* `POST /api/v1/exams`
* `POST /api/v1/exams/{id}/marks/bulk`
* `POST /api/v1/exams/{id}/results/calculate`
* `GET /api/v1/exams/{id}/report-cards`

Timetable:

* `POST /api/v1/timetable/generate`
* `POST /api/v1/timetable/substitute`
* `GET /api/v1/timetable/class/{class_id}`

Portals use scopes:

* parent can only access linked child records
* student can only access self
* teacher can access assigned classes/subjects
* admin has full scope via RBAC

## 7) SECURITY & ACCESS CONTROL

RBAC flow:

* `sms_permissions` defines atomic actions
* roles get permissions through `sms_role_permissions`
* users get roles through `sms_user_roles`
* menu entries reference permissions
* controller methods call `Permission::check('module.action')`

Data-level access:

* class teacher sees only assigned class/section
* parent sees only linked students
* teacher sees only subjects/classes in `sms_class_subjects` and `sms_class_teachers`
* branch isolation by `branch_id` in every query

Protection:

* passwords: `password_hash()` / `password_verify()`
* sessions for admin web UI
* JWT only for external/mobile APIs
* all SQL via prepared statements
* output escaped in views
* CSRF tokens on all forms
* file upload whitelist + randomized storage path
* sensitive fields can be encrypted at rest with `openssl` if needed
* use HTTPS, secure cookies, SameSite=Lax/Strict

Password reset:

* generate single-use token with expiry
* store hashed token
* invalidate on first use

## 8) KEY PHP CODE SKELETONS

### `app/Config/database.php`

```php
<?php
return [
    'host' => getenv('DB_HOST') ?: '127.0.0.1',
    'port' => getenv('DB_PORT') ?: '3306',
    'name' => getenv('DB_NAME') ?: 'sms_db',
    'user' => getenv('DB_USER') ?: 'root',
    'pass' => getenv('DB_PASS') ?: '',
    'charset' => 'utf8mb4',
];
```

### `app/Core/Database.php`

```php
<?php
final class Database {
    private static ?Database $instance = null;
    private \PDO $pdo;

    private function __construct(array $config) {
        $dsn = sprintf(
            "mysql:host=%s;port=%s;dbname=%s;charset=%s",
            $config['host'], $config['port'], $config['name'], $config['charset']
        );

        $this->pdo = new PDO($dsn, $config['user'], $config['pass'], [
            PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
            PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
            PDO::ATTR_EMULATE_PREPARES => false,
            PDO::ATTR_PERSISTENT => false,
        ]);
    }

    public static function instance(array $config): self {
        if (!self::$instance) self::$instance = new self($config);
        return self::$instance;
    }

    public function pdo(): PDO { return $this->pdo; }

    public function beginTransaction(): bool { return $this->pdo->beginTransaction(); }
    public function commit(): bool { return $this->pdo->commit(); }
    public function rollBack(): bool { return $this->pdo->rollBack(); }
}
```

### `app/Core/Model.php`

```php
<?php
abstract class Model {
    protected PDO $db;
    protected string $table;
    protected string $primaryKey = 'id';

    public function __construct(PDO $db) { $this->db = $db; }

    public function select(string $sql, array $params = []): array {
        $stmt = $this->db->prepare($sql);
        $stmt->execute($params);
        return $stmt->fetchAll();
    }

    public function findById(int $id): ?array {
        $stmt = $this->db->prepare("SELECT * FROM {$this->table} WHERE {$this->primaryKey} = :id AND deleted_at IS NULL LIMIT 1");
        $stmt->execute(['id' => $id]);
        $row = $stmt->fetch();
        return $row ?: null;
    }

    public function insert(array $data): int {
        $cols = array_keys($data);
        $fields = implode(',', array_map(fn($c) => "`$c`", $cols));
        $placeholders = implode(',', array_map(fn($c) => ":$c", $cols));
        $sql = "INSERT INTO {$this->table} ($fields) VALUES ($placeholders)";
        $stmt = $this->db->prepare($sql);
        $stmt->execute($data);
        return (int)$this->db->lastInsertId();
    }

    public function update(int $id, array $data): bool {
        $sets = implode(', ', array_map(fn($c) => "`$c` = :$c", array_keys($data)));
        $data['id'] = $id;
        $sql = "UPDATE {$this->table} SET $sets WHERE {$this->primaryKey} = :id";
        return $this->db->prepare($sql)->execute($data);
    }

    public function delete(int $id): bool {
        $stmt = $this->db->prepare("DELETE FROM {$this->table} WHERE {$this->primaryKey} = :id");
        return $stmt->execute(['id' => $id]);
    }

    public function softDelete(int $id): bool {
        $stmt = $this->db->prepare("UPDATE {$this->table} SET deleted_at = NOW() WHERE {$this->primaryKey} = :id");
        return $stmt->execute(['id' => $id]);
    }
}
```

### `app/Middleware/Permission.php`

```php
<?php
final class Permission {
    public static function check(string $permissionKey): void {
        if (empty($_SESSION['user_id'])) {
            http_response_code(401);
            exit('Unauthorized');
        }

        $permissions = $_SESSION['permissions'] ?? [];
        if (!in_array($permissionKey, $permissions, true)) {
            http_response_code(403);
            exit('Forbidden');
        }
    }
}
```

### `modules/auth/controllers/AuthController.php`

```php
<?php
final class AuthController {
    public function login(PDO $db): void {
        $username = trim($_POST['username'] ?? '');
        $password = $_POST['password'] ?? '';

        $stmt = $db->prepare("SELECT id, username, password_hash, status FROM sms_users WHERE username = :u OR email = :u OR phone = :u LIMIT 1");
        $stmt->execute(['u' => $username]);
        $user = $stmt->fetch();

        if (!$user || $user['status'] !== 'active' || !password_verify($password, $user['password_hash'])) {
            http_response_code(422);
            exit('Invalid credentials');
        }

        session_regenerate_id(true);
        $_SESSION['user_id'] = (int)$user['id'];

        $rolesStmt = $db->prepare("
            SELECT p.permission_key
            FROM sms_user_roles ur
            JOIN sms_role_permissions rp ON rp.role_id = ur.role_id
            JOIN sms_permissions p ON p.id = rp.permission_id
            WHERE ur.user_id = :uid
        ");
        $rolesStmt->execute(['uid' => $user['id']]);
        $_SESSION['permissions'] = array_column($rolesStmt->fetchAll(), 'permission_key');

        $db->prepare("UPDATE sms_users SET last_login_at = NOW() WHERE id = :id")->execute(['id' => $user['id']]);
        header('Location: /dashboard');
        exit;
    }

    public function logout(): void {
        session_destroy();
        header('Location: /login');
        exit;
    }
}
```

### Student admission flow

```php
<?php
final class AdmissionController {
    public function store(PDO $db, SmsService $sms, MailService $mail): void {
        $db->beginTransaction();

        try {
            $applicationId = (int)$_POST['application_id'];

            $appStmt = $db->prepare("SELECT * FROM sms_admission_applications WHERE id = :id FOR UPDATE");
            $appStmt->execute(['id' => $applicationId]);
            $application = $appStmt->fetch();

            if (!$application || $application['status'] !== 'approved') {
                throw new RuntimeException('Application is not approved.');
            }

            $data = json_decode($application['applicant_json'], true, 512, JSON_THROW_ON_ERROR);

            $admissionNo = $this->generateAdmissionNo($db, (int)$application['branch_id']);
            $rollNo = $this->generateRollNo($db, (int)$application['branch_id'], (int)$application['academic_year_id'], (int)$application['applied_class_id']);

            $userId = $this->createUserAccount($db, $data);
            $studentId = $this->createStudent($db, $application, $data, $userId, $admissionNo, $rollNo);

            $guardianId = $this->createGuardian($db, $data);
            $this->linkGuardian($db, $studentId, $guardianId, true);

            $db->prepare("INSERT INTO sms_student_lifecycle_events
                (student_id, event_type, to_class_id, effective_date, created_by)
                VALUES (:sid, 'admission', :class_id, CURDATE(), :creator)")
                ->execute([
                    'sid' => $studentId,
                    'class_id' => $application['applied_class_id'],
                    'creator' => $_SESSION['user_id'] ?? null,
                ]);

            $db->prepare("UPDATE sms_admission_applications SET status = 'approved' WHERE id = :id")
               ->execute(['id' => $applicationId]);

            $db->commit();

            $sms->send($data['guardian_phone'] ?? null, "Welcome to the school. Admission No: {$admissionNo}, Roll No: {$rollNo}");
            $mail->send($data['guardian_email'] ?? null, 'Admission Successful', "Your child has been admitted. Admission No: {$admissionNo}");

            echo json_encode(['success' => true, 'student_id' => $studentId]);
        } catch (Throwable $e) {
            if ($db->inTransaction()) $db->rollBack();
            http_response_code(500);
            echo $e->getMessage();
        }
    }

    private function generateAdmissionNo(PDO $db, int $branchId): string {
        return 'ADM-' . $branchId . '-' . date('YmdHis') . '-' . random_int(100, 999);
    }

    private function generateRollNo(PDO $db, int $branchId, int $yearId, int $classId): string {
        $stmt = $db->prepare("SELECT COALESCE(MAX(CAST(roll_no AS UNSIGNED)),0)+1 AS next_roll
                               FROM sms_students
                               WHERE branch_id = :b AND academic_year_id = :y AND current_class_id = :c
                               FOR UPDATE");
        $stmt->execute(['b' => $branchId, 'y' => $yearId, 'c' => $classId]);
        return (string)$stmt->fetchColumn();
    }

    private function createUserAccount(PDO $db, array $data): int { /* insert sms_users */ }
    private function createStudent(PDO $db, array $app, array $data, int $userId, string $admissionNo, string $rollNo): int { /* insert sms_students */ }
    private function createGuardian(PDO $db, array $data): int { /* insert sms_guardians */ }
    private function linkGuardian(PDO $db, int $studentId, int $guardianId, bool $primary): void { /* insert sms_student_guardians */ }
}
```

### Fee collection transaction handling

```php
<?php
final class FeeService {
    public function collect(PDO $db, int $invoiceId, int $studentId, float $amount, string $method, ?string $gatewayRef = null): int {
        $db->beginTransaction();

        try {
            $invoiceStmt = $db->prepare("SELECT * FROM sms_fee_invoices WHERE id = :id FOR UPDATE");
            $invoiceStmt->execute(['id' => $invoiceId]);
            $invoice = $invoiceStmt->fetch();

            if (!$invoice) throw new RuntimeException('Invoice not found.');
            if (in_array($invoice['status'], ['paid','cancelled'], true)) throw new RuntimeException('Invoice cannot be paid.');

            if ($gatewayRef) {
                $dup = $db->prepare("SELECT id FROM sms_fee_transactions WHERE gateway_ref = :r AND status = 'success' LIMIT 1");
                $dup->execute(['r' => $gatewayRef]);
                if ($dup->fetch()) throw new RuntimeException('Duplicate gateway callback.');
            }

            $txNo = 'TXN-' . date('YmdHis') . '-' . random_int(1000, 9999);

            $db->prepare("
                INSERT INTO sms_fee_transactions
                (transaction_no, invoice_id, student_id, amount, payment_method, gateway_ref, status, received_by, raw_response)
                VALUES (:txn, :invoice_id, :student_id, :amount, :method, :gateway_ref, 'success', :received_by, :raw_response)
            ")->execute([
                'txn' => $txNo,
                'invoice_id' => $invoiceId,
                'student_id' => $studentId,
                'amount' => $amount,
                'method' => $method,
                'gateway_ref' => $gatewayRef,
                'received_by' => $_SESSION['user_id'] ?? null,
                'raw_response' => json_encode(['source' => 'manual']),
            ]);

            $txnId = (int)$db->lastInsertId();

            $itemStmt = $db->prepare("SELECT id, amount, discount_amount, tax_amount FROM sms_fee_invoice_items WHERE invoice_id = :id");
            $itemStmt->execute(['id' => $invoiceId]);
            $items = $itemStmt->fetchAll();

            $remaining = $amount;
            foreach ($items as $item) {
                if ($remaining <= 0) break;
                $due = max(0, ((float)$item['amount'] + (float)$item['tax_amount']) - (float)$item['discount_amount']);
                $alloc = min($remaining, $due);

                $db->prepare("INSERT INTO sms_fee_payment_allocations (transaction_id, invoice_item_id, amount)
                              VALUES (:t, :i, :a)")
                   ->execute(['t' => $txnId, 'i' => $item['id'], 'a' => $alloc]);

                $remaining -= $alloc;
            }

            $paid = (float)$invoice['paid_amount'] + $amount;
            $outstanding = max(0, (float)$invoice['total_amount'] + (float)$invoice['late_fee_amount'] - $paid);
            $status = $outstanding <= 0 ? 'paid' : 'partially_paid';

            $db->prepare("UPDATE sms_fee_invoices
                          SET paid_amount = :paid, outstanding_amount = :outstanding, status = :status
                          WHERE id = :id")
               ->execute([
                   'paid' => $paid,
                   'outstanding' => $outstanding,
                   'status' => $status,
                   'id' => $invoiceId,
               ]);

            $db->prepare("
                INSERT INTO sms_account_transactions (txn_no, source_type, source_id, description, status, created_by)
                VALUES (:txn_no, 'fee_transaction', :source_id, 'Fee collection', 'posted', :user_id)
            ")->execute([
                'txn_no' => $txNo,
                'source_id' => $txnId,
                'user_id' => $_SESSION['user_id'] ?? null,
            ]);

            $accTxnId = (int)$db->lastInsertId();

            // Example double-entry:
            // Debit Cash/Bank, Credit Fee Income/Receivable
            $db->prepare("INSERT INTO sms_account_transaction_lines (account_transaction_id, account_head_id, debit, credit)
                          VALUES (:t, :h, :d, :c)")
               ->execute(['t' => $accTxnId, 'h' => 1, 'd' => $amount, 'c' => 0.00]);

            $db->prepare("INSERT INTO sms_account_transaction_lines (account_transaction_id, account_head_id, debit, credit)
                          VALUES (:t, :h, :d, :c)")
               ->execute(['t' => $accTxnId, 'h' => 2, 'd' => 0.00, 'c' => $amount]);

            $db->commit();
            return $txnId;
        } catch (Throwable $e) {
            if ($db->inTransaction()) $db->rollBack();
            throw $e;
        }
    }
}
```

## 9) REPORTS & NOTIFICATIONS MATRIX

Reports:

* Admission register: `sms_students` joined with `sms_student_guardians`, `sms_student_documents`
* Attendance defaulters: aggregate `sms_student_attendance`
* Fee outstanding: `sms_fee_invoices` where `outstanding_amount > 0`
* Collection report: `sms_fee_transactions` by date/branch/method
* Exam result sheet: `sms_exam_results` joined with `sms_students`
* Rank list: `sms_exam_results` ordered by `percentage desc`
* Timetable: `sms_timetable_slots`
* Hostel occupancy: `sms_hostel_allocations` vs `sms_hostel_beds`
* Library overdue: `sms_library_loans` where `returned_at is null and due_at < now()`
* Asset register: `sms_assets` with maintenance and depreciation
* Discipline report: `sms_discipline_incidents` + `sms_discipline_actions`

Notification triggers:

* Admission approved → parent/student welcome SMS/email
* Fee invoice issued → fee reminder
* Fee overdue → reminder/escalation
* Attendance below threshold → parent alert
* Homework assigned → student/parent alert
* Exam schedule published → student/parent alert
* Result published → parent/student alert
* Circular/announcement → audience scope
* Transport route changed → transport parents
* Hostel incident → parent + warden
* Discipline action → parent + admin

Template variables:
`{student_name}`, `{admission_no}`, `{roll_no}`, `{class_name}`, `{fee_amount}`, `{due_date}`, `{attendance_percent}`, `{exam_name}`, `{result_status}`

## 10) ASSUMPTIONS & EXTENSIBILITY

Assumptions:

* single institution, multi-branch ready
* PHP 8.1+, MySQL 8.0+
* hybrid app: server-rendered admin + REST APIs for portals/mobile
* academic year starts on April 1 by default
* attendance, fee, exam, timetable, hostel, transport, library, HRMS, alumni are all in scope
* payments may be manual or gateway-based
* report cards are PDF-first

Extensibility:

* add multi-tenant isolation by adding `tenant_id` to every table
* add mobile app through token-based API auth
* add AI features for attendance risk, fee risk, timetable optimization, and performance prediction
* add payroll later on top of `sms_employees`, `sms_account_heads`, and accounting tables
* add SSO/OAuth later by extending `sms_users`

## 11) IMPLEMENTATION ROADMAP

Phase 1: foundation

* database, auth, RBAC, institutions, branches, academic year, classes, sections, users, audit logs

Phase 2: student core

* admission, student profiles, guardians, documents, lifecycle, student portal basics

Phase 3: academics

* subjects, class mapping, curriculum, lesson plans, timetable, substitutions

Phase 4: attendance and exams

* attendance capture, analytics, assessments, marks, results, report cards

Phase 5: fees and finance

* fee structures, invoices, transactions, ledger, receipts, notifications

Phase 6: communications and portals

* SMS/email/push, circulars, parent/student dashboards

Phase 7: operational modules

* transport, hostel, library, inventory, assets, HRMS

Phase 8: enrichment

* homework, LMS, events, discipline, alumni

Parallel-safe work:

* transport/hostel/library can run alongside LMS/events/discipline after the core student model exists
* fee and exam can be built in parallel once student, class, section, and RBAC are stable
