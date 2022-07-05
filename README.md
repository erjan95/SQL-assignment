# SQL-assignment

SQL Assignment #1

#1

CREATE TABLE employers (
    Employer_ID INTEGER PRIMARY KEY,
    Full_Name TEXT,
    Joining_Date Date,
    Current_Position TEXT,
    Department TEXT,
    Assigned_Project TEXT
);

INSERT INTO employers (Department) VALUES ('IT Support');

SELECT * FROM employers;



#2

CREATE TABLE Services (
    Software_ID INTEGER PRIMARY KEY,
    Name TEXT,
    Category TEXT,
    Size INTEGER,
    Number_of_installments INTEGER
);

INSERT INTO Services (Category) VALUES ('A');

SELECT * FROM Services;


#3

CREATE TABLE Software_Requests (
    Employer_ID INTEGER PRIMARY KEY,
    Software_ID INTEGER,
    Request_Start_Date Date,
    Request_Close_Date Date,
    Status TEXT
);

SELECT * FROM Software_Requests;


#4

How can you make database consistent for ensuring when new request was inserted,
number of installments property of Software table should be increased value by one?

For a database to be consistent, data written to the database must be valid according to all defined rules, including constraints, transactions, triggers, or any other remaining combinations.

#5

Imagine a situation, new software was requested and related property of Software table
has been increased. But after a while, due to technical requirements, IT Teams were not
able to finish requests and made it invalid requests. How can you automate to update the
number of installments accordingly which means it will reduce value by the amount those
invalid closed requests?



SQL assignment#2

#1

SELECT album.ArtistId AS albums, artist.Name AS Artist_Name, album.Title AS Album_Name
    FROM albums AS album
    JOIN artists AS artist ON album.ArtistId = artist.ArtistId
    ORDER BY Artist_Name
    ;
    
#2

SELECT artists.Name as Artist_Name, COUNT(albums.ArtistId) as Album_Count, albums.Title as Album_Name
FROM artists
JOIN albums ON (artists.ArtistId = albums.ArtistId)
GROUP BY Album_Name
HAVING Album_Count >= 1
ORDER BY Album_Name DESC;


#3

SELECT artists.Name as Artist_Name FROM artists
WHERE artists.ArtistId NOT IN (SELECT albums.ArtistId FROM albums)
ORDER BY Artist_Name;

#4

SELECT artists.Name as Artist_Name, COUNT(albums.ArtistId) as No_of_albums
FROM artists
JOIN albums ON (artists.ArtistId = albums.ArtistId)
GROUP BY Artist_Name
ORDER BY No_of_albums DESC, Artist_Name ASC;


#5


SELECT artists.Name as Artist_Name, COUNT(albums.ArtistId) as No_of_albums
FROM artists
JOIN albums ON (artists.ArtistId = albums.ArtistId)
GROUP BY Artist_Name
HAVING No_of_albums >= 10
ORDER BY No_of_albums DESC, Artist_Name ASC;

#6

SELECT artists.Name as Artist_Name, COUNT(albums.ArtistId) as No_of_albums
FROM artists
JOIN albums ON (artists.ArtistId = albums.ArtistId)
GROUP BY Artist_Name
ORDER BY No_of_albums DESC
LIMIT 3;

#7

SELECT artists.Name as Artist_Name, albums.Title As Album_Title ,tracks.TrackId as Track
FROM artists
JOIN tracks
JOIN albums
WHERE Artist_Name = 'Santana'
ORDER BY Track;

#8

SELECT employees.EmployeeId as 'Employee ID',
    (SELECT employees.FirstName || employees.LastName) AS 'Employee Name',
    employees.Title AS 'Employee Title',
    employees.ReportsTo AS 'Manager ID',
    i.FirstName as 'Manager Name',
    i.Title as 'Manager Title'
    FROM employees
    INNER JOIN employees AS i ON i.EmployeeId = employees.ReportsTo;
    
#9

CREATE VIEW top_employees AS
    SELECT employees.EmployeeId as emp_id,
    (SELECT employees.FirstName || employees.LastName) AS 'emp_name',
    COUNT(customers.CustomerID) as cust_count
    FROM employees
    JOIN customers
    ON employees.EmployeeId = customers.SupportRepId
    ORDER BY emp_name;
    
SELECT * FROM top_employees;
DROP VIEW IF EXISTS top_employees;


#10

CREATE TRIGGER trigger_media BEFORE INSERT ON media_types
    BEGIN
        SELECT CASE
            WHEN Name NOT LIKE '%MP3%' THEN
            RAISE(ABORT, 'cannot be inserted')
        END;
    END
;


#11

??



CREATE TABLE employers (
    Employer_ID INTEGER PRIMARY KEY,
    Full_Name TEXT,
    Joining_Date Date,
    Current_Position TEXT,
    Department TEXT,
    Assigned_Project TEXT
);

INSERT INTO employers (Department) VALUES ('IT Support');
