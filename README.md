# sql_test
# Test 1.a
CREATE TABLE users (
  user_id int PRIMARY KEY, 
  username varchar(255));
  
 INSERT INTO users (user_id, username)
VALUES
  (1,'John Doe'),
  (2,'Jane Don'),
  (3, 'Alice Jones'),
  (4, 'Lisa Romero');
  
# Test 1.b
CREATE TABLE training_details (
  user_training int PRIMARY KEY, 
  user_id int,
  training_id int,
  training_date date);
  
  INSERT INTO training_details (user_training, user_id, training_id, training_date)
VALUES
   (1, 1, 1, '2015-08-02'),
  (2, 2, 1, '2015-08-03'),
  (3, 3, 2, '2015-08-02'),
  (4, 4, 2, '2015-08-04'),
  (5, 2, 2, '2015-08-03'),
  (6, 1, 1, '2015-08-02'),
  (7, 3, 2, '2015-08-04'),
  (8, 4, 3, '2015-08-03'),
  (9, 1, 4, '2015-08-03'),
  (10, 3, 1, '2015-08-02'),
  (11, 4, 2, '2015-08-04'),
  (12, 3, 2, '2015-08-02'),
  (13, 1, 1, '2015-08-02'),
  (14, 4, 3, '2015-08-03');
 
# Test 1
SELECT 
  a.user_id,
  a.username,
  b.training_id, 
  b.training_date AS training_date,
  COUNT(*) AS count
FROM 
  users AS a
  INNER JOIN training_details AS b ON a.user_id = b.user_id
GROUP BY 
  a.user_id, 
  a.username, 
  b.training_id, 
  b.training_date
HAVING 
  COUNT(*) > 1
ORDER BY 
  training_date DESC, 
  count DESC;
  
  # Test 2
 SELECT s.TestID, s.Student_name, s.Test_Score, s.TestDate
FROM Student_score AS s
JOIN (
    SELECT Student_name, MAX(TestDate) AS Latest_Test_Date
    FROM Student_score
    GROUP BY Student_name
) AS t
ON s.Student_name = t.Student_name AND s.TestDate = t.Latest_Test_Date
