--table creation for Beneficiaries

CREATE TABLE Beneficiaries (
    beneficiary_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    age INT NOT NULL CHECK (age >= 0),
    gender VARCHAR(10) NOT NULL,
    location VARCHAR(100) NOT NULL,
    household_size INT NOT NULL CHECK (household_size >= 0),
    health_status VARCHAR(255) NOT NULL
);

--inserting values into the table
INSERT INTO Beneficiaries (beneficiary_id, first_name, last_name, age, gender, location, household_size, health_status)
VALUES
(001, 'Jeff', 'Mwilolo', 54, 'Male', 'Toyoyo', 5, 'Stable'),
(002, 'Natalie', 'Njiu', 36, 'Female', 'Kiondo', 7, 'Underweight'),
(003, 'Eli', 'Kiongos', 23, 'Male', 'Ritichu', 6, 'Overweight'),
(004, 'John', 'Kibuchi', 34, 'Male', 'Zotini', 9, 'Malnutrition'),
(005, 'Janet', 'Esikucha', 43, 'Female', 'Toyoyo', 4, 'Overweight');

--displaying the values inputed into the beneficiaries table
SELECT *
FROM Beneficiaries;

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
--table creation for Nutrition_Programs

CREATE TABLE Nutrition_Programs (
    program_id INT PRIMARY KEY,
    program_name VARCHAR(100) NOT NULL,
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    description TEXT,
    target_group VARCHAR(50) NOT NULL
);

--inserting values into the table
INSERT INTO Nutrition_Programs (program_id, program_name, start_date, end_date, description, target_group)
VALUES
(1, 'Child Nutrition', '2024-01-01', '2024-06-01', 'A program to improve child nutrition.', 'Children'),
(2, 'Maternal Health', '2024-02-01', '2024-07-01', 'Focused on maternal nutritional needs.', 'Pregnant Women'),
(3, 'General Health', '2024-03-01', '2024-08-01', 'General health improvement for adults.', 'Adults');

--displaying values in the Nutrition_Programs
SELECT *
FROM Nutrition_Programs;

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

--table creation for Food_Items

CREATE TABLE Food_Items (
    food_item_id INT PRIMARY KEY,
    food_item_name VARCHAR(100) NOT NULL UNIQUE
);

--inserting values into the table
INSERT INTO Food_Items (food_item_id, food_item_name)
VALUES
(1, 'Rice'),
(2, 'Maize Flour'),
(3, 'Green grams'),
(4, 'Milk Powder'),
(5, 'Vitamin Supplements');

--displaying values entered into the table
SELECT *
FROM Food_Items;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

--table creation for Food_Distribution

CREATE TABLE Food_Distribution (
    distribution_id INT PRIMARY KEY,
    program_id INT NOT NULL,
    beneficiary_id INT NOT NULL,
    distribution_date DATE NOT NULL,
    food_item_id INT NOT NULL,
    quantity INT NOT NULL CHECK (quantity > 0),
    FOREIGN KEY (program_id) REFERENCES Nutrition_Programs(program_id) ON DELETE CASCADE,
    FOREIGN KEY (beneficiary_id) REFERENCES Beneficiaries(beneficiary_id) ON DELETE CASCADE,
    FOREIGN KEY (food_item_id) REFERENCES Food_Items(food_item_id) ON DELETE CASCADE
);

--inserting values into the Food_Distribution table
INSERT INTO Food_Distribution (distribution_id, program_id, beneficiary_id, distribution_date, food_item_id, quantity)
VALUES
(1, 1, 1, '2024-01-15', 1, 10), -- Jeff receives Rice under Child Nutrition
(2, 1, 2, '2024-01-20', 2, 15), -- Natalie receives Maize Flour under Child Nutrition
(3, 2, 3, '2024-02-15', 4, 8),  -- Eli receives Milk Powder under Maternal Health
(4, 3, 4, '2024-03-10', 5, 5),  -- John receives Vitamin Supplements under General Health
(5, 1, 5, '2024-01-25', 3, 20); -- Janet receives Green grams under Child Nutrition

--displaying values of the Food_Distribution table
SELECT *
FROM Food_Distribution;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-- table creation for Health_Metrics

CREATE TABLE Health_Metrics (
    metric_id INT PRIMARY KEY,
    beneficiary_id INT NOT NULL,
    date_recorded DATE NOT NULL,
    BMI DECIMAL(5,2),
    anemia_status VARCHAR(50),
    malnutrition_status VARCHAR(50),
    FOREIGN KEY (beneficiary_id) REFERENCES Beneficiaries(beneficiary_id) ON DELETE CASCADE
);

--insering values into the  Health_Metrics table
INSERT INTO Health_Metrics(metric_id, beneficiary_id, date_recorded, BMI, anemia_status, malnutrition_status)
VALUES
(1, 1, '2024-02-01', 22.5, 'None', 'None'), -- Jeff's health data
(2, 2, '2024-02-10', 17.0, 'Mild', 'Moderate'), -- Natalie's health data
(3, 3, '2024-02-15', 18.5, 'Severe', 'None'), -- Eli's health data
(4, 4, '2024-03-01', 16.0, 'None', 'Severe'), -- John's health data
(5, 5, '2024-03-15', 23.0, 'None', 'None');  -- Janet's health data

--displaying values of thr Health_Metrics table
SELECT *
FROM Health_Metrics;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-- table creation for Program_Effectiveness

CREATE TABLE Program_Effectiveness (
    effectiveness_id INT PRIMARY KEY,
    program_id INT NOT NULL,
    reach INT NOT NULL CHECK (reach >= 0),
    coverage_area VARCHAR(100),
    outcome VARCHAR(255),
    FOREIGN KEY (program_id) REFERENCES Nutrition_Programs(program_id) ON DELETE CASCADE
);
