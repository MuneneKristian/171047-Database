--table for Beneficiaries

CREATE TABLE Beneficiaries (
    beneficiary_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    age INT NOT NULL CHECK (age >= 0),
    gender VARCHAR(10) NOT NULL,
    location VARCHAR(100) NOT NULL,
    household_size INT NOT NULL CHECK (household_size >= 0),
    health_status VARCHAR(255) NOT NULL
);
