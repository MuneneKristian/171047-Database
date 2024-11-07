--table creation for Beneficiaries

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
-- Table: Nutrition_Programs
CREATE TABLE Nutrition_Programs (
    program_id INT PRIMARY KEY AUTO_INCREMENT,
    program_name VARCHAR(100) NOT NULL,
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    description TEXT,
    target_group VARCHAR(50) NOT NULL
);

-- Table: Food_Items
CREATE TABLE Food_Items (
    food_item_id INT PRIMARY KEY AUTO_INCREMENT,
    food_item_name VARCHAR(100) NOT NULL UNIQUE
);

