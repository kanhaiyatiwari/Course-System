# Course Monitoring System

<p align="center">
  <img src="https://kanhaiyatiwari.github.io/media/corse.png" alt="Course Monitoring System" width="650">
</p>

<p align="center">
  <a href="https://drive.google.com/file/d/1ZF4kyBSPT5hKE6x21arHrypFql6X3qna/view"><b>Demo video</b></a> ·
  <a href="#setup--installation">Run locally</a> ·
  <a href="#database-design">Database design</a>
</p>

## Project Description

A console application for training institutes to plan and track their courses. The administrator manages courses, faculty, batches and day-wise course plans, and the faculty fill in what they taught each day. The goal is to see, for every batch, how far the course has progressed against the plan.

Solo project built in 5 days at Masai School.

## Tech Stack

| Area | Tools |
|---|---|
| Language | Java 17 |
| Database access | JDBC (MySQL Connector/J 8) |
| Database | MySQL |
| Design | DAO pattern, custom exceptions |
| Tools | Eclipse / Spring Tool Suite, Git |

## Key Features

**Administrator**
- Log in with admin credentials
- Create, update and view courses
- Create batches, set batch size and start date, and allocate faculty to a batch
- Add and update faculty
- Create day-wise course plans for each batch
- View the day-wise progress of every batch and generate a report per batch

**Faculty**
- Log in with their username and password
- View the course plan for their batch
- Fill in the day-wise planner (topic and status)
- Change their password

**Engineering**
- DAO layer (`AdministratorDao`, `Facultydao`) keeps all SQL out of the menu code
- Custom exceptions for each entity (`CourseException`, `BatchException`, ...)
- Foreign keys between course, faculty, batch and course plan tables

## Database Design

![Table schema](course_monitoring_system/src/tableSchema.png)

Tables: `administrator`, `course`, `faculty`, `batch`, `CoursPlan`. The full SQL is in [`course_monitoring_system/src/mysql.txt`](course_monitoring_system/src/mysql.txt).

## Setup & Installation

**Prerequisites:** Java 17, MySQL 8, [MySQL Connector/J 8](https://dev.mysql.com/downloads/connector/j/)

1. Clone the repository
   ```bash
   git clone https://github.com/kanhaiyatiwari/Course-System.git
   cd Course-System/course_monitoring_system
   ```
2. Create the database and tables
   ```sql
   CREATE DATABASE cm;
   USE cm;
   -- then run the statements in src/mysql.txt
   INSERT INTO administrator VALUES ('admin', 'admin');
   ```
3. Set your MySQL username and password in `src/com/masai/utility/Dbutily.java`
   ```java
   String url = "jdbc:mysql://localhost:3306/cm";
   conn = DriverManager.getConnection(url, "root", "your_password");
   ```
4. Compile and run (replace the path with your Connector/J jar)
   ```bash
   javac -cp path/to/mysql-connector-j-8.0.31.jar -d bin $(find src -name "*.java")
   java -cp "bin:path/to/mysql-connector-j-8.0.31.jar" com.usecases.Main
   ```
   On Windows use `;` instead of `:` in the classpath. You can also import the folder into Eclipse or STS as an existing project, add the connector jar to the build path and run `Main`.
5. Choose `0` for Administrator or `1` for Faculty and follow the menu.

## Author

**Kanhaiya Lal Tiwari** · [Portfolio](https://kanhaiyatiwari.github.io/) · [LinkedIn](https://www.linkedin.com/in/kanhaiya-tiwari-684942257/)
