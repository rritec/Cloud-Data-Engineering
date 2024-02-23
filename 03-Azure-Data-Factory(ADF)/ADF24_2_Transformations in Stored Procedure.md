# Workingdays Transformations in Functions and Stored Procedure



## Create required data
``` sql
drop table new_table;
GO;
-- Create a new table
CREATE TABLE new_table
(
    ordered_date DATE,
    promised_date DATE
);
GO;
-- Insert data into the new_table
INSERT INTO new_table (ordered_date, promised_date)
VALUES
    ('2024-01-01', '2024-02-01'),
    ('2024-01-02', '2024-02-01'),
    ('2024-01-03', '2024-02-01'),
    ('2024-01-04', '2024-02-01'),
    ('2024-01-05', '2024-02-01'),
    ('2024-01-06', '2024-02-01'),
    ('2024-01-07', '2024-02-01'),
    ('2024-01-08', '2024-02-01'),
    ('2024-01-09', '2024-02-01'),
    ('2024-01-10', '2024-02-01'),
    ('2024-01-11', '2024-02-01'),
    ('2024-01-12', '2024-02-01'),
    ('2024-01-13', '2024-02-01'),
    ('2024-01-14', '2024-02-01'),
    ('2024-01-15', '2024-02-01'),
    ('2024-01-16', '2024-02-01'),
    ('2024-01-17', '2024-02-01'),
    ('2024-01-18', '2024-02-01'),
    ('2024-01-19', '2024-02-01'),
    ('2024-01-20', '2024-02-01'),
    ('2024-01-21', '2024-02-01'),
    ('2024-01-22', '2024-02-01'),
    ('2024-01-23', '2024-02-01'),
    ('2024-01-24', '2024-02-01'),
    ('2024-01-25', '2024-02-01'),
    ('2024-01-26', '2024-02-01'),
    ('2024-01-27', '2024-02-01'),
    ('2024-01-28', '2024-02-01'),
    ('2024-01-29', '2024-02-01'),
    ('2024-01-30', '2024-02-01'),
    ('2024-01-31', '2024-02-01'),
    ('2024-02-01', '2024-02-01'),
    ('2024-02-02', '2024-02-01'),
    ('2024-02-03', '2024-02-01'),
    ('2024-02-04', '2024-02-01'),
    ('2024-02-05', '2024-02-01'),
    ('2024-02-06', '2024-02-01'),
    ('2024-02-07', '2024-02-01'),
    ('2024-02-08', '2024-02-01'),
    ('2024-02-09', '2024-02-01'),
    ('2024-02-10', '2024-02-01'),
    ('2024-02-11', '2024-02-01'),
    ('2024-02-12', '2024-02-01'),
    ('2024-02-13', '2024-02-01'),
    ('2024-02-14', '2024-02-01'),
    ('2024-02-15', '2024-02-01'),
    ('2024-02-16', '2024-02-01'),
    ('2024-02-17', '2024-02-01'),
    ('2024-02-18', '2024-02-01'),
    ('2024-02-19', '2024-02-01'),
    ('2024-02-20', '2024-02-01'),
    ('2024-02-21', '2024-02-01'),
    ('2024-02-22', '2024-02-01'),
    ('2024-02-23', '2024-02-01'),
    ('2024-02-24', '2024-02-01'),
    ('2024-02-25', '2024-02-01'),
    ('2024-02-26', '2024-02-01'),
    ('2024-02-27', '2024-02-01'),
    ('2024-02-28', '2024-02-01'),
    ('2024-02-29', '2024-02-01'),
    ('2024-03-01', '2024-02-01'),
    ('2024-03-02', '2024-02-01'),
    ('2024-03-03', '2024-02-01'),
    ('2024-03-04', '2024-02-01'),
    ('2024-03-05', '2024-02-01'),
    ('2024-03-06', '2024-02-01'),
    ('2024-03-07', '2024-02-01'),
    ('2024-03-08', '2024-02-01'),
    ('2024-03-09', '2024-02-01'),
    ('2024-03-10', '2024-02-01'),
    ('2024-03-11', '2024-02-01'),
    ('2024-03-12', '2024-02-01'),
    ('2024-03-13', '2024-02-01'),
    ('2024-03-14', '2024-02-01'),
    ('2024-03-15', '2024-02-01'),
    ('2024-03-16', '2024-02-01'),
    ('2024-03-17', '2024-02-01'),
    ('2024-03-18', '2024-02-01'),
    ('2024-03-19', '2024-02-01'),
    ('2024-03-20', '2024-02-01'),
    ('2024-03-21', '2024-02-01'),
    ('2024-03-22', '2024-02-01'),
    ('2024-03-23', '2024-02-01'),
    ('2024-03-24', '2024-02-01'),
    ('2024-03-25', '2024-02-01'),
    ('2024-03-26', '2024-02-01'),
    ('2024-03-27', '2024-02-01'),
    ('2024-03-28', '2024-02-01'),
    ('2024-03-29', '2024-02-01'),
    ('2024-03-30', '2024-02-01'),
    ('2024-03-31', '2024-02-01');
```


## Create target table
``` sql
Drop table results_table
```
``` sql
-- Create a new table to store results
CREATE TABLE results_table
(
    ordered_date DATE,
    promised_date DATE,    
    workingdays INT
);
```
## create Function
``` sql
DROP FUNCTION dbo.CalculateWorkingDays;
GO;
```
``` sql
-- Create FUNCTION
CREATE FUNCTION dbo.CalculateWorkingDays
(
    @startDate DATE,
    @endDate DATE
)
RETURNS INT
AS
BEGIN
    DECLARE @workingDays INT = 0;
    DECLARE @currentDate DATE = @startDate;
    DECLARE @targetDate DATE = @endDate;

    WHILE @currentDate <> @targetDate
    BEGIN
        -- Exclude weekends (Saturday and Sunday)
        IF DATEPART(WEEKDAY, @currentDate) NOT IN (1, 7)
        BEGIN
            SET @workingDays = @workingDays + 1;
        END

        -- Move to the next day
        IF @startDate < @endDate
            SET @currentDate = DATEADD(DAY, 1, @currentDate);
        ELSE
            SET @currentDate = DATEADD(DAY, -1, @currentDate);
    END

    -- Include the end date if it's not a weekend
    IF DATEPART(WEEKDAY, @targetDate) NOT IN (1, 7)
    BEGIN
        SET @workingDays = @workingDays + 1;
    END

    RETURN IIF(@startDate <= @endDate, @workingDays, -@workingDays);
END;
```
## Create Stored Procedure

1. create Stored procedure inside database

``` sql
DROP PROCEDURE CalculateWorkingDaysForTable
```
``` sql
-- Create a stored procedure to calculate working days
CREATE PROCEDURE CalculateWorkingDaysForTable
AS
BEGIN
    -- Declare variables
    DECLARE @ordered_date DATE;
    DECLARE @promised_date DATE;    
    DECLARE @workingdays INT;

    -- Cursor to iterate through new_table
    DECLARE workingDaysCursor CURSOR FOR
        SELECT ordered_date, promised_date
        FROM new_table;

    -- Open the cursor
    OPEN workingDaysCursor;

    -- Fetch the first row
    FETCH NEXT FROM workingDaysCursor INTO @ordered_date, @promised_date;

    -- Loop through the rows
    WHILE @@FETCH_STATUS = 0
    BEGIN
        -- Calculate working days using your logic (considering holidays)
        SET @workingdays = dbo.CalculateWorkingDays(@ordered_date, @promised_date);

        -- Insert the result into results_table
        INSERT INTO results_table (ordered_date, promised_date,  workingdays)
        VALUES (@ordered_date, @promised_date, @workingdays);

        -- Fetch the next row
        FETCH NEXT FROM workingDaysCursor INTO @ordered_date, @promised_date;
    END

    -- Close and deallocate the cursor
    CLOSE workingDaysCursor;
    DEALLOCATE workingDaysCursor;
END;
```
## Call this Stored procedure and verify results
``` sql
-- Call the stored procedure
EXEC CalculateWorkingDaysForTable
GO

select ordered_date,promised_date,workingdays from results_table

```
## Map this stored procedure in ADF

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/34935fa4-9b74-4d0e-ac16-be5def3e95a9)

4. Run and observe it.
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/5833de7f-ac19-4845-803b-82161e952769)

5. 
## Questions
## Answers
