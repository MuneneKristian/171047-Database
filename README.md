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

-- Table: Food_Distribution
CREATE TABLE Food_Distribution (
    distribution_id INT PRIMARY KEY AUTO_INCREMENT,
    program_id INT NOT NULL,
    beneficiary_id INT NOT NULL,
    distribution_date DATE NOT NULL,
    food_item_id INT NOT NULL,
    quantity INT NOT NULL CHECK (quantity > 0),
    FOREIGN KEY (program_id) REFERENCES Nutrition_Programs(program_id) ON DELETE CASCADE,
    FOREIGN KEY (beneficiary_id) REFERENCES Beneficiaries(beneficiary_id) ON DELETE CASCADE,
    FOREIGN KEY (food_item_id) REFERENCES Food_Items(food_item_id) ON DELETE CASCADE
);
-- Table: Health_Metrics
CREATE TABLE Health_Metrics (
    metric_id INT PRIMARY KEY AUTO_INCREMENT,
    beneficiary_id INT NOT NULL,
    date_recorded DATE NOT NULL,
    BMI DECIMAL(5,2),
    anemia_status VARCHAR(50),
    malnutrition_status VARCHAR(50),
    FOREIGN KEY (beneficiary_id) REFERENCES Beneficiaries(beneficiary_id) ON DELETE CASCADE
);
