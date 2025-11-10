# Names : HABANABASHAKA Philimin
# Id : 27487
  



# Student Performance Tracker (PL/SQL Collections, Records, and GOTO)

# Overview
This project demonstrates the use of **PL/SQL Collections**, **Records**, and **GOTO statements** in a real-world scenario — a simple *Student Performance Tracker*.  
It processes student data, calculates average marks, determines academic status, and handles invalid records gracefully using a GOTO control structure.
# Design Notes

## Purpose
This project demonstrates the integration of **PL/SQL Collections**, **Records**, and **GOTO statements** through a Student Performance Tracking system.

## Design Highlights
- **Record (student_rec):**
  - Stores individual student details: ID, Name, Average Marks, Failed Subjects, and Status.
- **Collection (student_table):**
  - Acts as an in-memory list of student records for batch processing.
- **GOTO Statement:**
  - Used sparingly to skip processing when a record is invalid (e.g., missing student name).

## Logic Flow
1. Fetch all students with their marks using a cursor.
2. For each student:
   - Calculate average mark and failed subjects.
   - Use GOTO to skip incomplete data.
   - Determine status based on performance.
3. Display all processed records using `DBMS_OUTPUT`.

## Design Justification
- **Associative Array:** Fast, index-based in-memory processing.
- **Record:** Clean, structured way to store related fields.
- **GOTO:** Demonstrates control transfer, but intentionally limited to one clear case.

## Collection

A collection in PL/SQL is like a list or array that can store multiple values of the same type (for example, a list of numbers or names).
It helps you handle many items together instead of one at a time.

Example:
A list of student marks stored in memory.

## Record

A record is like a row of data that can store different types of information together (like a mini table row).
It can hold related fields such as a student’s ID, name, and average mark — all in one variable.

Example:
One record might store:
(ID = 1, Name = 'Alice', Average = 85)

##  GOTO

A GOTO statement is used to jump to a specific part of a PL/SQL program using a label.
It can skip over or jump to certain code sections — but it should be used carefully because it can make code harder to read.

Example:
If data is invalid, use GOTO skip_this; to jump to a label named skip_this.

# Reflection and Learning

## What I Learned
- How to use **Collections** to hold multiple rows temporarily in PL/SQL.
- How **Records** simplify grouping related data.
- How **GOTO** works — and why it's usually avoided in large systems.

## Challenges Faced
- Handling NULL values correctly.
- Designing the cursor query to include averages and failure counts.
- Understanding when GOTO is appropriate versus using IF conditions.

## Improvements for the Future
- Replace GOTO with structured exception handling.
- Add user input or parameters for dynamic execution.
- Store output in a result table instead of using DBMS_OUTPUT.


##  Key Concepts
- **Collections:** Used an **Associative Array** to store multiple student records in memory.
- **Records:** Defined a **custom RECORD type** to hold individual student information.
- **GOTO Statement:** Used to skip invalid or incomplete data entries during processing.

## File Structure
| File | Description |
|------|--------------|
| `scripts/create_tables.sql` | Creates required database tables. |
| `scripts/insert_sample_data.sql` | Inserts test data. |
| `scripts/student_tracker.sql` | Main PL/SQL program logic. |
| `docs/design_notes.md` | Explains design decisions. |
| `docs/reflection.md` | Reflection on learning outcomes. |
| `docs/output_sample.txt` | Example execution output. |

## How to Run
1. Open SQL*Plus, Oracle SQL Developer, or any PL/SQL IDE.
2. Run:
   ```sql
   @scripts/create_tables.sql
   @scripts/insert_sample_data.sql
   @scripts/student_tracker.sql



   SET SERVEROUTPUT ON;

   
---

## 📜 scripts/create_tables.sql

```sql
-- Drop existing tables (if any)
BEGIN
  EXECUTE IMMEDIATE 'DROP TABLE marks';
  EXECUTE IMMEDIATE 'DROP TABLE students';
EXCEPTION
  WHEN OTHERS THEN NULL;
END;
/

-- Create main tables
CREATE TABLE students (
  student_id NUMBER PRIMARY KEY,
  student_name VARCHAR2(50)
);

CREATE TABLE marks (
  student_id NUMBER,
  subject VARCHAR2(30),
  mark NUMBER(3),
  CONSTRAINT fk_student FOREIGN KEY (student_id)
    REFERENCES students(student_id)
);
/



## 📜 scripts/student_tracker.sql

SET SERVEROUTPUT ON;

DECLARE
  -- Define a record type for one student's info
  TYPE student_rec IS RECORD (
    student_id   students.student_id%TYPE,
    student_name students.student_name%TYPE,
    avg_mark     NUMBER(5,2),
    failed_subj  NUMBER,
    status       VARCHAR2(20)
  );

  -- Define a collection (Associative Array)
  TYPE student_table IS TABLE OF student_rec INDEX BY PLS_INTEGER;
  students_data student_table;

  v_counter INTEGER := 0;

  CURSOR c_students IS
    SELECT s.student_id,
           s.student_name,
           NVL(AVG(m.mark),0) AS avg_mark,
           SUM(CASE WHEN m.mark < 40 THEN 1 ELSE 0 END) AS failed_subj
    FROM students s
    LEFT JOIN marks m ON s.student_id = m.student_id
    GROUP BY s.student_id, s.student_name;

BEGIN
  FOR rec IN c_students LOOP
    v_counter := v_counter + 1;

    -- GOTO example: Skip student if name is NULL
    IF rec.student_name IS NULL THEN
      DBMS_OUTPUT.PUT_LINE('Skipping invalid student record...');
      GOTO skip_student;
    END IF;

    students_data(v_counter).student_id   := rec.student_id;
    students_data(v_counter).student_name := rec.student_name;
    students_data(v_counter).avg_mark     := rec.avg_mark;
    students_data(v_counter).failed_subj  := rec.failed_subj;

    IF rec.failed_subj > 2 THEN
      students_data(v_counter).status := 'At Risk';
    ELSE
      students_data(v_counter).status := 'Good Standing';
    END IF;

    DBMS_OUTPUT.PUT_LINE('Processed: ' || rec.student_name ||
                         ' | Avg: ' || rec.avg_mark ||
                         ' | Status: ' || students_data(v_counter).status);

    <<skip_student>>
    NULL; -- Label for GOTO
  END LOOP;

EXCEPTION
  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE('Error occurred: ' || SQLERRM);
END;
/


