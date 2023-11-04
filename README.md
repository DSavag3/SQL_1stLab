# SQL_1stLab

This is my table with my two added movies and their corresponding values.

mysql> select * from movies;
+-------------------------+---------+-------------+------------+--------+
| title                   | runtime | genre       | IMDB_Score | rating |
+-------------------------+---------+-------------+------------+--------+
| Howard the Duck         |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula             |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers       |     129 | Sci-Fi      |        7.2 | PG-13  |
| Waltz With Bashir       |      90 | Documentary |        8.0 | R      |
| Spaceballs              |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.           |      92 | Animation   |        8.1 | G      |
| Fast and Furious Five   |     130 | Action      |        7.3 | PG-13  |
| Five Nights at Freddy's |     110 | Horror      |        5.6 | PG-13  |
+-------------------------+---------+-------------+------------+--------+

QUestion 2

mysql> SELECT * FROM movies WHERE genre = 'Sci-Fi';
+-------------------+---------+--------+------------+--------+
| title             | runtime | genre  | IMDB_Score | rating |
+-------------------+---------+--------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi |        4.6 | PG     |
| Starship Troopers |     129 | Sci-Fi |        7.2 | PG-13  |
+-------------------+---------+--------+------------+--------+

Question 3

mysql> SELECT * FROM movies WHERE IMDB_Score >= 6.5;
+-----------------------+---------+-------------+------------+--------+
| title                 | runtime | genre       | IMDB_Score | rating |
+-----------------------+---------+-------------+------------+--------+
| Starship Troopers     |     129 | Sci-Fi      |        7.2 | PG-13  |
| Waltz With Bashir     |      90 | Documentary |        8.0 | R      |
| Spaceballs            |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.         |      92 | Animation   |        8.1 | G      |
| Fast and Furious Five |     130 | Action      |        7.3 | PG-13  |
+-----------------------+---------+-------------+------------+--------+

Question 4

mysql> SELECT * FROM movies WHERE (rating = 'G' OR rating = 'PG') AND runtime < 100;
+---------------+---------+-----------+------------+--------+
| title         | runtime | genre     | IMDB_Score | rating |
+---------------+---------+-----------+------------+--------+
| Spaceballs    |      96 | Comedy    |        7.1 | PG     |
| Monsters Inc. |      92 | Animation |        8.1 | G      |
+---------------+---------+-----------+------------+--------+

Question 5

mysql> SELECT genre, AVG(runtime) AS average_runtime
    -> FROM movies
    -> WHERE IMDB_Score < 7.5
    -> GROUP BY genre;
+--------+-----------------+
| genre  | average_runtime |
+--------+-----------------+
| Sci-Fi |        119.5000 |
| Horror |         96.5000 |
| Comedy |         96.0000 |
| Action |        130.0000 |
+--------+-----------------+

Question 6

mysql> UPDATE movies
    -> SET rating = 'R'
    -> WHERE title = 'Starship Troopers';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM movies;
+-------------------------+---------+-------------+------------+--------+
| title                   | runtime | genre       | IMDB_Score | rating |
+-------------------------+---------+-------------+------------+--------+
| Howard the Duck         |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula             |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers       |     129 | Sci-Fi      |        7.2 | R      |
| Waltz With Bashir       |      90 | Documentary |        8.0 | R      |
| Spaceballs              |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.           |      92 | Animation   |        8.1 | G      |
| Fast and Furious Five   |     130 | Action      |        7.3 | PG-13  |
| Five Nights at Freddy's |     110 | Horror      |        5.6 | PG-13  |
+-------------------------+---------+-------------+------------+--------+
8 rows in set (0.00 sec)

Question 7

mysql> SELECT title, runtime, genre, IMDB_Score, rating
    -> FROM movies
    -> WHERE genre IN ('Horror', 'Documentary');
+-------------------------+---------+-------------+------------+--------+
| title                   | runtime | genre       | IMDB_Score | rating |
+-------------------------+---------+-------------+------------+--------+
| Lavalantula             |      83 | Horror      |        4.7 | TV-14  |
| Waltz With Bashir       |      90 | Documentary |        8.0 | R      |
| Five Nights at Freddy's |     110 | Horror      |        5.6 | PG-13  |
+-------------------------+---------+-------------+------------+--------+

Question 8

mysql> SELECT rating, AVG(IMDB_Score) AS average_IMDB_score, MAX(IMDB_Score) AS max_IMDB_score, MIN(IMDB_Score) AS min_IMDB_score
    -> FROM movies
    -> GROUP BY rating;
+--------+--------------------+----------------+----------------+
| rating | average_IMDB_score | max_IMDB_score | min_IMDB_score |
+--------+--------------------+----------------+----------------+
| PG     |            5.85000 |            7.1 |            4.6 |
| TV-14  |            4.70000 |            4.7 |            4.7 |
| R      |            7.60000 |            8.0 |            7.2 |
| G      |            8.10000 |            8.1 |            8.1 |
| PG-13  |            6.45000 |            7.3 |            5.6 |
+--------+--------------------+----------------+----------------+

Question 9

mysql> SELECT rating, AVG(IMDB_Score) AS average_IMDB_score, MAX(IMDB_Score) AS max_IMDB_score, MIN(IMDB_Score) AS min_IMDB_score
    -> FROM movies
    -> GROUP BY rating
    -> HAVING COUNT(*) > 1;
+--------+--------------------+----------------+----------------+
| rating | average_IMDB_score | max_IMDB_score | min_IMDB_score |
+--------+--------------------+----------------+----------------+
| PG     |            5.85000 |            7.1 |            4.6 |
| R      |            7.60000 |            8.0 |            7.2 |
| PG-13  |            6.45000 |            7.3 |            5.6 |
+--------+--------------------+----------------+----------------+

Question 10

mysql> DELETE FROM movies
    -> WHERE rating = 'R';
Query OK, 2 rows affected (0.02 sec)

mysql> SELECT * FROM movies;
+-------------------------+---------+-----------+------------+--------+
| title                   | runtime | genre     | IMDB_Score | rating |
+-------------------------+---------+-----------+------------+--------+
| Howard the Duck         |     110 | Sci-Fi    |        4.6 | PG     |
| Lavalantula             |      83 | Horror    |        4.7 | TV-14  |
| Spaceballs              |      96 | Comedy    |        7.1 | PG     |
| Monsters Inc.           |      92 | Animation |        8.1 | G      |
| Fast and Furious Five   |     130 | Action    |        7.3 | PG-13  |
| Five Nights at Freddy's |     110 | Horror    |        5.6 | PG-13  |
+-------------------------+---------+-----------+------------+--------+


Group A Work

mysql> CREATE TABLE cars (
    ->     ID INT AUTO_INCREMENT,
    ->     year INT,
    ->     make VARCHAR(255),
    ->     model VARCHAR(255),
    ->     PRIMARY KEY (ID)
    -> );
Query OK, 0 rows affected (0.50 sec)

mysql> describe cars;
+-------+--------------+------+-----+---------+----------------+
| Field | Type         | Null | Key | Default | Extra          |
+-------+--------------+------+-----+---------+----------------+
| ID    | int          | NO   | PRI | NULL    | auto_increment |
| year  | int          | YES  |     | NULL    |                |
| make  | varchar(255) | YES  |     | NULL    |                |
| model | varchar(255) | YES  |     | NULL    |                |
+-------+--------------+------+-----+---------+----------------+

mysql> Select * FROM cars;
+----+------+-----------+---------+
| ID | year | make      | model   |
+----+------+-----------+---------+
|  1 | 2010 | Toyota    | Corolla |
|  2 | 2015 | Honda     | Civic   |
|  3 | 2018 | Ford      | Fusion  |
|  4 | 2019 | Chevrolet | Camaro  |

mysql> SELECT * FROM cars WHERE year BETWEEN 2010 AND 2018;
+----+------+--------+---------+
| ID | year | make   | model   |
+----+------+--------+---------+
|  1 | 2010 | Toyota | Corolla |
|  2 | 2015 | Honda  | Civic   |
|  3 | 2018 | Ford   | Fusion  |
+----+------+--------+---------+

mysql> SELECT * FROM cars GROUP BY ID ORDER BY year DESC;
+----+------+-----------+---------+
| ID | year | make      | model   |
+----+------+-----------+---------+
|  4 | 2019 | Chevrolet | Camaro  |
|  3 | 2018 | Ford      | Fusion  |
|  2 | 2015 | Honda     | Civic   |
|  1 | 2010 | Toyota    | Corolla |
+----+------+-----------+---------+


mysql> SELECT COUNT(*) AS car_count FROM cars;
+-----------+
| car_count |
+-----------+
|         4 |
+-----------+
