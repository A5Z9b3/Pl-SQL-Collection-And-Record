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

