# Lab6 SQL Procedure README

## Overview

This Lab6.txt script, authored by Sujan Rokad on November 07, 2023, focuses on modifying the structure of the master table, adding new data, and creating a stored procedure named `purge_customer`. The procedure is designed to delete records from the master table based on a specified cutoff date.

## Procedure Details

1. **Alter Table:**
   - Added a new column, `last_activity_date` (type DATE), to the existing `customers` table, allowing NULL values.

2. **Update Records:**
   - Utilized UPDATE statements to populate the `last_activity_date` column for each master record. Ensured unique dates within the last 2 years.

3. **Insert New Record:**
   - Added a new record to the master table with `last_activity_date` more than 3 years ago. No corresponding records were inserted into the sales table.

4. **Stored Procedure: purge_customer**
   - Accepts two parameters: `@cut_off_date` (DATE) and `@update` (INT, default value of 0).
   - If `@update` is 1, deletes records from the master table where `last_activity_date` is before `@cut_off_date`.
   - If `@update` is not 1, prints a message and displays records from the master table that would be deleted.

## Verification

Added verification code to the script to test the stored procedure:

```sql
-- Verification
PRINT 'Verify procedure'
PRINT 'Master Table Before Changes'
SELECT * FROM dbo.customers 
Exec purge_customer @cut_off_date = '2020-11-07', @update = 0
PRINT 'After 1st Call To Procedure'
SELECT * FROM dbo.customers
Exec purge_customer @cut_off_date = '2020-11-07', @Update = 1
PRINT 'After 2nd Call To Procedure'
SELECT * FROM dbo.customers 
