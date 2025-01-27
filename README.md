# SQL Databases: Concepts and Techniques

This repository is dedicated to providing a comprehensive guide and set of examples for working with **SQL databases**. It covers a variety of topics, from database creation to advanced topics like **normalization** and optimizing queries. Whether you're just getting started with relational databases or looking to enhance your skills, this resource has you covered.

## Table of Contents
- [Overview](#overview)
- [Key Concepts](#key-concepts)
- [Database Design](#database-design)
- [Normalization](#normalization)
- [Usage](#usage)
- [Example](#example)
- [Requirements](#requirements)
- [Contributing](#contributing)
- [License](#license)

## Overview

SQL (Structured Query Language) is the standard language used for managing and manipulating relational databases. This repository includes information on creating, querying, and manipulating SQL databases, with a strong focus on **database design** and **normalization** techniques. It covers best practices for designing efficient databases and the importance of data integrity.

### Topics Covered:
- Introduction to SQL and relational databases
- Database design fundamentals
- SQL queries (SELECT, INSERT, UPDATE, DELETE)
- Advanced SQL topics (joins, subqueries, indexing)
- Database normalization (1NF, 2NF, 3NF, BCNF)

## Key Concepts

### 1. **Database Basics**
   - **Tables**: Structure that stores data in rows and columns.
   - **Primary Key**: A unique identifier for each row in a table.
   - **Foreign Key**: A reference to a primary key in another table.
   - **Relationships**: The connections between tables, typically via foreign keys.
   
### 2. **SQL Queries**
   - **SELECT**: Retrieves data from one or more tables.
   - **INSERT**: Adds new data to a table.
   - **UPDATE**: Modifies existing data in a table.
   - **DELETE**: Removes data from a table.

### 3. **Joins**
   - **INNER JOIN**: Returns records that have matching values in both tables.
   - **LEFT JOIN**: Returns all records from the left table and the matched records from the right table.
   - **RIGHT JOIN**: Returns all records from the right table and the matched records from the left table.
   - **FULL JOIN**: Returns records when there is a match in one of the tables.

### 4. **Indexes**
   - An index is a data structure that improves the speed of data retrieval operations on a table.

## Database Design

Effective database design is crucial for the success of an application. Proper design ensures data consistency, reduces redundancy, and simplifies querying.

### Key Principles:
1. **Entity-Relationship (ER) Model**: A diagram that shows the relationships between entities (tables) in a database.
2. **Schemas**: The blueprint that defines the structure of the database, including tables, fields, and relationships.
3. **Data Integrity**: Ensuring accuracy and consistency of data across the database.

## Normalization

Normalization is the process of organizing the attributes and tables of a relational database to minimize redundancy and dependency. The goal of normalization is to reduce the chances of data anomalies.

### The Normal Forms (NF):
Normalization typically involves organizing the data into different "normal forms," each one addressing a specific issue related to redundancy or dependency.

#### 1. **First Normal Form (1NF)**
   - Ensures that each table column contains atomic (indivisible) values.
   - Removes repeating groups or arrays.
   
   **Example:**
   - A table with multiple phone numbers in a single column would violate 1NF. Each phone number should be placed in a separate row.

#### 2. **Second Normal Form (2NF)**
   - Achieved by meeting all requirements of 1NF.
   - All non-key attributes must be fully functionally dependent on the entire primary key.
   - Removes partial dependencies.

   **Example:**
   - In a table where a composite primary key (e.g., `StudentID` and `CourseID`) is used, if a non-key attribute depends only on part of the composite key (e.g., `StudentName` depends only on `StudentID`), this violates 2NF.

#### 3. **Third Normal Form (3NF)**
   - Achieved by meeting all requirements of 2NF.
   - No transitive dependencies (i.e., non-key attributes should not depend on other non-key attributes).
   
   **Example:**
   - If `EmployeeAddress` depends on `EmployeeID`, and `EmployeeID` depends on `DepartmentID`, then `EmployeeAddress` indirectly depends on `DepartmentID`. This would violate 3NF, and `EmployeeAddress` should be moved to a separate table.

#### 4. **Boyce-Codd Normal Form (BCNF)**
   - A stronger version of 3NF.
   - Every determinant must be a candidate key.
   
   **Example:**
   - A table with a candidate key that isn't a superkey would violate BCNF. For example, if `RoomNumber` determines `BuildingName`, and `BuildingName` is not a candidate key, then the table would violate BCNF.

### Benefits of Normalization:
- **Eliminates redundancy**: Reduces data duplication across the database.
- **Improves consistency**: Helps ensure data integrity and consistency.
- **Optimizes queries**: More efficient data retrieval by organizing the data into smaller, more manageable tables.

## Usage

To apply normalization techniques, start by creating a simple database and then apply each normalization step. Here's an example of how you might start with a denormalized table and gradually normalize it.

```sql
-- Example: Denormalized table
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    CourseName VARCHAR(100),
    InstructorName VARCHAR(100)
);

-- Step 1: Convert to 1NF (Remove repeating groups)
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(100),
    InstructorName VARCHAR(100)
);

CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);

-- Step 2: Convert to 2NF (Remove partial dependencies)
-- Already satisfied by the new schema structure.

-- Step 3: Convert to 3NF (Remove transitive dependencies)
-- Already satisfied by the new schema structure.
