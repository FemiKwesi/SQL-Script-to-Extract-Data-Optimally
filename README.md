![Screenshot to show how optimal creating an  INDEX  is](https://user-images.githubusercontent.com/112349616/187793961-234ea459-a367-4826-8f68-5267a1c0abd3.png)
# SQL-Script-to-Extract-Data-Optimally
The goal of this project is to show how 
creating an "INDEX" can optimize the search 
for data where there are millions of 
records.

SOLUTION

STEP 1
Create a schema in the database with the below query
CREATE SCHEMA Clock_Problem

STEP 2
Create table in the database with below query
CREATE TABLE `clock_problem`.`clock_degrees` (
  `idClock_Degrees` INT NOT NULL AUTO_INCREMENT,
  `Hours` TIME(2) NOT NULL,
  `Minutes` TIME(2) NOT NULL,
  PRIMARY KEY (`idClock_Degrees`),
  UNIQUE INDEX `idClock_Degrees_UNIQUE` (`idClock_Degrees` ASC) VISIBLE);

STEP 3
Insert values into columns, this can be done in two ways individually (A)  and in bulk (B). B is more efficient than A as it saves time.

A
Less efficient
INSERT INTO `clock_problem`.`clock_degrees` (`idClock_Degrees`,`Hours`, `Minutes`) VALUES (30,1,00);
INSERT INTO `clock_problem`.`clock_degrees` (`idClock_Degrees`,`Hours`, `Minutes`) VALUES (60,2,00);
INSERT INTO `clock_problem`.`clock_degrees` (`idClock_Degrees`,`Hours`, `Minutes`) VALUES (90,3,00);
INSERT INTO `clock_problem`.`clock_degrees` (`idClock_Degrees`,`Hours`, `Minutes`) VALUES (180,6,00);
INSERT INTO `clock_problem`.`clock_degrees` (`idClock_Degrees`,`Hours`, `Minutes`) VALUES (236,7,56);

B
More efficient
 INSERT INTO `clock_problem`.`clock_degrees` (`idClock_Degrees`,`Hours`, `Minutes`) VALUES 
(2,"",""),
(3,"",""),
(4,"","");
(30,1,00),
(60,2,00),
 (90,3,00),
 (180,6,00),
 (236,7,56);

FINAL SOLUTION
STEP 4
There are two solutions to get our final solution  (A)  and solution (B)

Solution  (A)   is a less efficient way to get an optimal execution of the query. This solution took 0.063 seconds to run

(A)
SELECT idClock_Degrees, Hours, Minutes
FROM
clock_problem.clock_degrees
WHERE clock_degrees.Hours AND clock_degrees.Minutes IS NOT NULL;

(B)
Solution  (B)  is a more efficient way to get an optimal execution of the query. This solution took 0.015 seconds to run.
This solution requires that we first and foremost create an index on the three columns and then use the where function to filter out the empty/null values in s second query.
CREATE INDEX clock_index ON clock_problem.clock_degrees(idClock_Degrees,Hours,Minutes);
SELECT * FROM clock_problem.clock_degrees WHERE clock_degrees.Hours AND clock_degrees.Minutes IS NOT NULL;
