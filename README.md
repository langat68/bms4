# bms4

-- Create the database
CREATE DATABASE IF NOT EXISTS blood_donor_system;
USE blood_donor_system;

-- Create donors table
CREATE TABLE IF NOT EXISTS donors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    phone VARCHAR(20) NOT NULL,
    blood_type ENUM('A+', 'A-', 'B+', 'B-', 'AB+', 'AB-', 'O+', 'O-') NOT NULL,
    medical_history TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create donations table
CREATE TABLE IF NOT EXISTS donations (
    id INT AUTO_INCREMENT PRIMARY KEY,
    donor_id INT NOT NULL,
    donation_date DATE NOT NULL,
    quantity_ml INT NOT NULL,
    FOREIGN KEY (donor_id) REFERENCES donors(id) ON DELETE CASCADE
);

-- Create admin table
CREATE TABLE IF NOT EXISTS admins (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL
);

-- Insert a default admin (password is 'admin123')
INSERT INTO admins (username, password) VALUES ('admin', '$2b$10$VX5M6zZzQZQZQZQZQZQZQeQZQZQZQZQZQZQZQZQZQZQZQZQZQZQZQ');

SELECT * FROM donors;
UPDATE admins 
SET password = '$2b$10$EO7/PH5qQYgeWjlFmbCdfOMAq/XmLsQDsRSYVghE4nul9C0Hfgx5e' 
WHERE username = 'admin';
SELECT * FROM admins WHERE username = 'admin';



