# Pl-SQL-Collection-And-Record

# Student Performance Tracker (PL/SQL Collections, Records, and GOTO)

# Overview
This project demonstrates the use of **PL/SQL Collections**, **Records**, and **GOTO statements** in a real-world scenario — a simple *Student Performance Tracker*.  
It processes student data, calculates average marks, determines academic status, and handles invalid records gracefully using a GOTO control structure.

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

