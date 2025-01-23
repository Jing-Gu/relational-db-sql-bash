# Learn SQL by Building a Student Database: Part 1
Create a Bash script that uses SQL to enter information about your computer science students into PostgreSQL.

## Key points
- Given the csv files, how to use bash scripts to run SQL that insert data into PostgresSQL DB ? Check `insert_data.sh` bash scripting.
- SQL commands: CREATE, ALTER, INSERT...
- Dump the db into a sql file using `pg_dump`

```sql
psql --username=freecodecamp --dbname=postgres
CREATE DATABASE students;
\c students

CREATE TABLE students();
CREATE TABLE majors();
CREATE TABLE courses();
CREATE TABLE majors_courses();

ALTER TABLE students ADD COLUMN student_id SERIAL PRIMARY KEY;
ALTER TABLE students ADD COLUMN first_name VARCHAR(50) NOT NULL;
ALTER TABLE students ADD COLUMN last_name VARCHAR(50) NOT NULL;
ALTER TABLE students ADD COLUMN major_id INT;
ALTER TABLE students ADD COLUMN gpa NUMERIC(2,1);

ALTER TABLE majors ADD COLUMN major_id SERIAL PRIMARY KEY;
ALTER TABLE majors ADD COLUMN major VARCHAR(50) NOT NULL;

ALTER TABLE students ADD FOREIGN KEY(major_id) REFERENCES majors(major_id);

ALTER TABLE courses ADD COLUMN course_id SERIAL PRIMARY KEY;
ALTER TABLE courses ADD COLUMN course VARCHAR(100) NOT NULL;

ALTER TABLE majors_courses ADD COLUMN major_id INT;
ALTER TABLE majors_courses ADD FOREIGN KEY(major_id) REFERENCES majors(major_id);
ALTER TABLE majors_courses ADD COLUMN course_id INT;
ALTER TABLE majors_courses ADD FOREIGN KEY(course_id) REFERENCES courses(course_id);
ALTER TABLE majors_courses ADD PRIMARY KEY(major_id, course_id);

INSERT INTO majors(major) VALUES('Database Administration');
INSERT INTO courses(course) VALUES('Data Structures and Algorithms');
INSERT INTO students(first_name, last_name, major_id, gpa) VALUES('Rhea', 'Kellems', 1, 2.5);

```

```bash
# dump the students database into a students.sql file

pg_dump --clean --create --inserts --username=freecodecamp students > students.sql
```
