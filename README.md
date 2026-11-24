1-
CREATE TABLE Employees
(
    ID INT,
    Name VARCHAR(100),
    Salary DECIMAL(10,2)
);


*********************************************************
2-
ALTER TABLE Employees
ADD Department VARCHAR(50);
**********************************************************
3-
ALTER TABLE Employees
DROP COLUMN Salary;
*******************************************************
4-
EXEC sp_rename  'Employees.Department','DeptName','COLUMN';
************************
5-
CREATE TABLE Projects
(
    ProjectID INT,
    ProjectName VARCHAR(100)
);
**************************************************
6-
ALTER TABLE Employees
ADD CONSTRAINT PK_Employees
PRIMARY KEY (ID);
******************************************
7-
ALTER TABLE Projects
ADD CONSTRAINT PK_Projects
PRIMARY KEY (ProjectID);

ALTER TABLE Employees
ADD ProjectID INT;

ALTER TABLE Employees
ADD CONSTRAINT FK_Employees_Projects
FOREIGN KEY (ProjectID)
REFERENCES Projects(ProjectID);
**************************************************
8-
ALTER TABLE Employees
DROP CONSTRAINT FK_Employees_Projects;
**************************************************
9-
CREATE TABLE Customers
(
    CustomerID INT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100),
    Status VARCHAR(20)
);
*******************************************************
10-
CREATE TABLE Customers
(
    CustomerID INT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100),
    Status VARCHAR(20)
);
***********************************************************
11-
ALTER TABLE Customers
ADD CONSTRAINT UQ_Customers_FullName
UNIQUE (FirstName, LastName);
*************************************************************
12-
ALTER TABLE Customers
ADD CONSTRAINT DF_Customers_Status
DEFAULT 'Active' FOR Status;
*********************************************************
13-
CREATE TABLE Orders
(
    OrderID INT,
    CustomerID INT,
    OrderDate DATETIME,
    TotalAmount DECIMAL(12,2)
);
***********************************************************
14-
ALTER TABLE Orders
ADD CONSTRAINT CK_Orders_TotalAmount
CHECK (TotalAmount > 0);
*********************************************************
15-
CREATE SCHEMA Sales;
GO

ALTER SCHEMA Sales
TRANSFER dbo.Orders;
*************************************************************
16-
EXEC sp_rename
    'Sales.Orders',
    'SalesOrders';
********************************************************************
Data Manipulation Language (DML)

1-
SELECT Name, Salary
FROM Employees;
---------------------
2-
SELECT Name, Salary
FROM Employees;
----------------------
3-
SELECT DISTINCT DeptName
FROM Employees;
-----------------------
4-
SELECT TOP 5 *
FROM Employees;

----------------------------
5-
SELECT *
FROM Employees
ORDER BY Salary DESC;
----------------------------------
6-
SELECT *
FROM Employees
ORDER BY ID
OFFSET 2 ROWS
FETCH NEXT 10 ROWS ONLY;
-------------------------------
7-
SELECT AVG(Salary) AS AverageSalary
FROM Employees;
-----------------------------------------
8-
SELECT
    MAX(Salary) AS MaximumSalary,
    MIN(Salary) AS MinimumSalary
FROM Employees;
-------------------------------------
9-
SELECT TOP 3 *
FROM Employees
ORDER BY Salary DESC;
-----------------------------
10-
SELECT *
FROM Employees
ORDER BY Name ASC;
-------------------------
11-
SELECT *
FROM Employees
ORDER BY Salary DESC
OFFSET 1 ROWS
FETCH NEXT 5 ROWS ONLY;
-----------------------------------
12-
SELECT SUM(Salary) AS TotalSalary
FROM Employees;
----------------------------------
13-
SELECT *
FROM Employees
WHERE Salary BETWEEN 40000 AND 60000
ORDER BY Salary ASC;
