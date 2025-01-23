CREATE DATABASE record_company;

-- select db which is to be worked on
USE record_company;

ALTER TABLE test
ADD another_column VARCHAR(255); 
DROP TABLE albums;	

CREATE TABLE bands(
id INT NOT NULL AUTO_INCREMENT,
name VARCHAR(255) not null,
PRIMARY KEY (id)
);

CREATE TABLE albums(
id INT NOT NULL AUTO_INCREMENT,
name VARCHAR(255) NOT NULL,
release_year INT,
band_id INT NOT NULL,
PRIMARY KEY (id),
FOREIGN KEY (band_id) REFERENCES bands(id) 
);

INSERT INTO bands (name) 
VALUES ('Iron Maiden');

INSERT INTO bands(name)
VALUES ('Deuce'),('Avendedd Sevenfold'),('Ankor');

SELECT * FROM bands; 
SELECT * FROM bands LIMIT 2;
SELECT name FROM bands;
SELECT id AS 'ID', name AS 'Band Name'
FROM bands;
SELECT * FROM bands ORDER BY name;

INSERT INTO albums (name,release_year,band_id)
VALUES ('The Number of the Beasts',1985,1),		
		('Power Slave',1984,1),
        ('Nightmare',2018,2),
        ('Nightmare',2010,3),
        ('Test Album',NULL,3);
        
SELECT * FROM albums;

SELECT DISTINCT name FROM albums;

-- where is uded to filter the items from database 
UPDATE albums 
SET release_year = 1982
WHERE id  = 1;

SELECT * FROM albums 
WHERE release_year < 2000;

-- check wether the letters are with in the string
-- % sign used to check letters in between
SELECT * FROM albums
WHERE name LIKE '%er%' OR band_id = 2;

SELECT * FROM albums
WHERE release_year = 1984 AND band_id = 1;

SELECT * FROM albums
WHERE release_year BETWEEN 2000 AND 2018;

SELECT * FROM albums
WHERE release_year IS NULL;

DELETE FROM albums WHERE id = 5;

-- join method joins the two tables
-- inner join same as join it only returns the same elements in the left side and right side of Join method (bands JOIN albums)  ,
-- left join it return s all the elements of table on left side   , 
-- right join it returns all the elements of right sie of table

SELECT * FROM bands
INNER JOIN albums ON bands.id = albums.band_id; 

SELECT * FROM bands
LEFT JOIN albums ON bands.id = albums.band_id; 

SELECT * FROM albums
RIGHT JOIN bands ON bands.id = albums.band_id; 

-- Aggrregate Functions
SELECT AVG(release_year) FROM albums;
SELECT SUM(release_year) FROM albums;

SELECT band_id, COUNT(band_id) FROM albums
GROUP BY band_id; 

SELECT b.name AS band_name, COUNT(a.id) AS num_albums
FROM bands AS b
LEFT JOIN albums AS a ON b.id = a.band_id
GROUP BY b.id;

SELECT b.name AS band_name, COUNT(a.id) AS num_albums
FROM bands AS b
LEFT JOIN albums AS a ON b.id = a.band_id
WHERE b.name = 'Deuce'
GROUP BY b.id
HAVING num_albums = 1;


