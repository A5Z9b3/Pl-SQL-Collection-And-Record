# Pl-SQL-Collection-And-Record

# Student Performance Tracker (PL/SQL Collections, Records, and GOTO)

## 📘 Overview
This project demonstrates the use of **PL/SQL Collections**, **Records**, and **GOTO statements** in a real-world scenario — a simple *Student Performance Tracker*.  
It processes student data, calculates average marks, determines academic status, and handles invalid records gracefully using a GOTO control structure.

## 🧩 Key Concepts
- **Collections:** Used an **Associative Array** to store multiple student records in memory.
- **Records:** Defined a **custom RECORD type** to hold individual student information.
- **GOTO Statement:** Used to skip invalid or incomplete data entries during processing.

## 🗂️ File Structure
| File | Description |
|------|--------------|
| `scripts/create_tables.sql` | Creates required database tables. |
| `scripts/insert_sample_data.sql` | Inserts test data. |
| `scripts/student_tracker.sql` | Main PL/SQL program logic. |
| `docs/design_notes.md` | Explains design decisions. |
| `docs/reflection.md` | Reflection on learning outcomes. |
| `docs/output_sample.txt` | Example execution output. |

## ▶️ How to Run
1. Open SQL*Plus, Oracle SQL Developer, or any PL/SQL IDE.
2. Run:
   ```sql
   @scripts/create_tables.sql
   @scripts/insert_sample_data.sql
   @scripts/student_tracker.sql



   SET SERVEROUTPUT ON;

