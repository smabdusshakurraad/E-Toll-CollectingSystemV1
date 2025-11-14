# 🛣️ E-Toll-CollectingSystemV1 - JAVA
## 📝 Overview

This project is a **Toll System Management Application** developed as a desktop application using **Java Swing/AWT** for the graphical user interface. It is designed to manage toll plazas, vehicle registrations, and user administration, with all data stored in a **MySQL database**.

It includes forms for adding new tolls (`AddToll`), registering vehicles (`AddVehicle`), and an administrative panel (`Admin`) for navigation.

## ⚙️ Technologies Used

* **Language:** Java
* **GUI Framework:** Java Swing / AWT
* **Database:** MySQL
* **Database Driver:** MySQL Connector/J (JDBC)

---

## 🚀 Setup and Run Instructions

This guide ensures you have the correct Java version and database setup to successfully run the application.

### 1. Java Runtime Environment (JRE)

The application was compiled using a newer JDK (Class File Version 69.0), so you must use a compatible JRE.

| Component | Required Version |
| :--- | :--- |
| **JDK/JRE** | **Java 18 or newer** |

**Action:** Ensure your IntelliJ IDEA project's SDK and your run configuration's JRE are set to **Java 25** (or the latest version available).

### 2. Database Setup

The application connects to a database named `toll_sys` using the `DbConnection.java` class.

#### **A. Database Credentials Check**

Open `DbConnection.java` and **verify or update** the connection details:

```java
// ... inside DbConnection.java
DB_URL = "jdbc:mysql://localhost:3306/toll_sys";
USER = "root";       // Change this if your MySQL user is different
PASS = "YOUR_MYSQL_PASSWORD"; // <--- CRUCIAL: Add your MySQL password here!


B. Create Database and Tables

Use your MySQL console or a database management tool to execute the following SQL commands:
SQL

-- 1. Create the database
CREATE DATABASE IF NOT EXISTS toll_sys;
USE toll_sys;

-- 2. Create the 'toll' table (Used by AddToll.java)
CREATE TABLE IF NOT EXISTS toll (
    id INT AUTO_INCREMENT PRIMARY KEY,
    place VARCHAR(255) NOT NULL UNIQUE,
    price DECIMAL(10, 2) NOT NULL
);

-- 3. Create the 'vehicle' table (Used by AddVehicle.java)
CREATE TABLE IF NOT EXISTS vehicle (
    id INT AUTO_INCREMENT PRIMARY KEY,
    brandName VARCHAR(255),
    vehicleModel VARCHAR(255),
    vehicleNumber VARCHAR(255) UNIQUE,
    vClass VARCHAR(255),
    vType VARCHAR(255)
);

-- 4. Create the 'user' table (Required for Admin and Login)
CREATE TABLE IF NOT EXISTS user (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    isAdmin BOOLEAN DEFAULT FALSE
);

-- Insert a default Admin user for initial login
INSERT INTO user (username, password, isAdmin) VALUES ('admin', 'admin123', TRUE);


This is a comprehensive README.md file for your Java Toll System project.

It covers the project summary, required technology, and the step-by-step instructions needed to resolve the Java version and database connection errors you encountered.
Markdown

# 🛣️ Toll System Management Application

## 📝 Overview

This project is a **Toll System Management Application** developed as a desktop application using **Java Swing/AWT** for the graphical user interface. It is designed to manage toll plazas, vehicle registrations, and user administration, with all data stored in a **MySQL database**.

It includes forms for adding new tolls (`AddToll`), registering vehicles (`AddVehicle`), and an administrative panel (`Admin`) for navigation.

## ⚙️ Technologies Used

* **Language:** Java
* **GUI Framework:** Java Swing / AWT
* **Database:** MySQL
* **Database Driver:** MySQL Connector/J (JDBC)

---

## 🚀 Setup and Run Instructions

This guide ensures you have the correct Java version and database setup to successfully run the application.

### 1. Java Runtime Environment (JRE)

The application was compiled using a newer JDK (Class File Version 69.0), so you must use a compatible JRE.

| Component | Required Version |
| :--- | :--- |
| **JDK/JRE** | **Java 25 or newer** |

**Action:** Ensure your IntelliJ IDEA project's SDK and your run configuration's JRE are set to **Java 25** (or the latest version available).

### 2. Database Setup

The application connects to a database named `toll_sys` using the `DbConnection.java` class.

#### **A. Database Credentials Check**

Open `DbConnection.java` and **verify or update** the connection details:

```java
// ... inside DbConnection.java
DB_URL = "jdbc:mysql://localhost:3306/toll_sys";
USER = "root";       // Change this if your MySQL user is different
PASS = "YOUR_MYSQL_PASSWORD"; // <--- CRUCIAL: Add your MySQL password here!

B. Create Database and Tables

Use your MySQL console or a database management tool to execute the following SQL commands:
SQL

-- 1. Create the database
CREATE DATABASE IF NOT EXISTS toll_sys;
USE toll_sys;

-- 2. Create the 'toll' table (Used by AddToll.java)
CREATE TABLE IF NOT EXISTS toll (
    id INT AUTO_INCREMENT PRIMARY KEY,
    place VARCHAR(255) NOT NULL UNIQUE,
    price DECIMAL(10, 2) NOT NULL
);

-- 3. Create the 'vehicle' table (Used by AddVehicle.java)
CREATE TABLE IF NOT EXISTS vehicle (
    id INT AUTO_INCREMENT PRIMARY KEY,
    brandName VARCHAR(255),
    vehicleModel VARCHAR(255),
    vehicleNumber VARCHAR(255) UNIQUE,
    vClass VARCHAR(255),
    vType VARCHAR(255)
);

-- 4. Create the 'user' table (Required for Admin and Login)
CREATE TABLE IF NOT EXISTS user (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    isAdmin BOOLEAN DEFAULT FALSE
);

-- Insert a default Admin user for initial login
INSERT INTO user (username, password, isAdmin) VALUES ('admin', 'admin123', TRUE);

3. JDBC Driver Configuration (Fixing "No suitable driver found")

The java.sql.SQLException is caused by the missing MySQL JDBC driver (MySQL Connector/J) in the classpath.

Action:

    Download the MySQL Connector/J JAR file (e.g., mysql-connector-java-X.X.XX.jar).

    In IntelliJ IDEA: Go to File > Project Structure > Modules > Dependencies and use the + button to add the downloaded JAR file to your project's module dependencies.

4. Running the Application

Once the database and driver are configured, run the main class. (Assuming the main entry class is named Toll or Home):
Method	Command
IntelliJ IDEA	Select the main class (Toll or Home) in your Run Configuration and click the Run button.
Command Line	java -cp ".:mysql-connector-java-*.jar" Toll (Mac/Linux)
Command Line	java -cp ".;mysql-connector-java-*.jar" Toll (Windows)

🔒 Initial Credentials

Use the following credentials to log into the Admin Panel after setup:
Role	Username	Password
Admin	admin	admin123


📄 Project Structure (Core Files)

File Name	Description
Admin.java	The main administrative panel/dashboard of the application.
AddToll.java	GUI form and logic for adding new toll places and prices to the toll table.
AddVehicle.java	GUI form and logic for registering new vehicles to the vehicle table.
DbConnection.java	Handles the JDBC connection, queries (getData), and updates (updateDB) for the MySQL database.
logo.png	Application icon/logo displayed on the frames.
Other missing files	Likely Home.java (the main entry point/login screen), TollList.java, UpdateToll.java, UsersList.java, and TransactionList.java

