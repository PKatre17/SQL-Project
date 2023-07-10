# Database management system for a rental company
Designed a Database Management System using SQL for a rental company. This design of the database includes a conceptual model, logical model, data dictionary, and the queries used to design the database.

## Conceptual Model
The conceptual diagram has eight entities all having a properly defined relationship. From the multiple relation types, mostly the many-to-many, optional, and mandatory ones are used to create and show the link between the entities.

<img width="556" alt="Screenshot 2023-07-10 at 12 17 56 PM" src="https://github.com/PKatre17/SQL-Project/assets/97483777/4b3a7586-73a2-4612-a43e-850f01b74dc2">

## Logical Model
A logical diagram is needed because we can use the foreign and primary key here which is not present in the conceptual diagram. In a logical diagram, we are working on attributes whereas in conceptual we are using entities. In this logical diagram, the rental entity clustering is where all the entities are linked to the rental entities. In order to receive payment the rental has to know which rental got on rent. It has the category id to identify.

<img width="576" alt="Screenshot 2023-07-10 at 12 21 14 PM" src="https://github.com/PKatre17/SQL-Project/assets/97483777/8bb07fc3-b6c7-4a29-b7a1-4962454b9ba2">

## Data Dictionary

Refer to the project report attached above "DBMS project.pdf"

## SQL Queries
Till now we just created the design of the database. Now to make its functionality work we have implemented the database in SQL. In SQL varieties we have chosen the MySQL database

We have 13 entities so we created 13 tables in MySQL with the correct data type occupying each column. When we are creating our tables, it is important to also establish the relationship that an entity might have with another entity, which is portrayed by primary keys and foreign keys.

### Below are a few of the queries used to Create the tables in the database:

- Creating Customer Table:

CREATE TABLE Customer(
`CustomerID` INT NOT NULL, `CustomerName` VARCHAR(45) NOT NULL, `Phone` DOUBLE NULL,
`Zipcode` INT NOT NULL,
PRIMARY KEY (`CustomerID`));

- Creating Customer Support Table:

CREATE TABLE Customer Support ( `CustomerID` INT NOT NULL, `ProductID` INT NOT NULL, `TicketID` INT NOT NULL, PRIMARY KEY (`CustomerID`));

- Creating ItemReturn Table:

CREATE TABLE ItemReturn (
`ProductID` INT NOT NULL,
`PaymentID` INT NOT NULL,
`Return_Date` DATE NOT NULL,
`Return_time` TIME NOT NULL, `Transaction_Status` VARCHAR(45) NOT NULL, PRIMARY KEY (`ProductID`));

### Below are a few of the queries used to Insert the data into the tables:

- Inserting data into Rental Table:
  
INSERT INTO Rental(CategoryID,CustomerID, ProductID,Electronics) VALUES (01,111,1001,'iPhone 13 pro');

INSERT INTO Rental(CategoryID,CustomerID, ProductID,Furniture) VALUES (02,112,1002,'Folding chair');

INSERT INTO Rental(CategoryID,CustomerID, ProductID,Vehicles) VALUES (03,113,1003,'Kia K5');

INSERT INTO Rental(CategoryID,CustomerID, ProductID,Sports) VALUES (04,114,1004,'Basket Ball');

INSERT INTO Rental(CategoryID,CustomerID, ProductID,Clothing) VALUES (05,115,1005,'Bell bottom Trouser');

INSERT INTO Rental(CategoryID,CustomerID, ProductID,Home) VALUES (06,116,1006,'Washing Machine');

INSERT INTO Rental(CategoryID,CustomerID, ProductID,Electronics,Vehicle) VALUES (07,117,1007,'Samsung Galaxy S6','Volkswagen polo');

### Below are a few of the queries used to Query the data in the database:

- Finding Product ID for the item with refund processed on a specific date.
  
SELECT i.ProductID

FROM item return AS i

WHERE i.Transaction_Status = 'Refund Processed' AND i.Return_Date = '2022-02-05'

- Retrieving Customer name and Product ID using joins between rental and customer table on Customer ID

SELECT Customer.CustomerName as Name,
 
Rental.ProductID AS ProdID

FROM Customer

JOIN Rental ON rental.CustomerID = customer.CustomerID;

- Retrieving Payment details of customers where payment date is greater than return date 2022-02-05

SELECT *

FROM Payment

WHERE Payment_Date >
(SELECT Return_Date from ItemReturn WHERE Return_Date = '2022-02-05');

- Retrieving count of employees who worked dates between 1st Jan 2022 and 1st June 2022
  
SELECT COUNT(Employee_name) FROM Cleaning

WHERE Cleaning_Date

BETWEEN '2022-01-01' AND '2022-06-01' Group BY Employee_name;
