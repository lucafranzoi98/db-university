1. > 160 results
SELECT *
FROM `students`
WHERE `date_of_birth`
LIKE '1990-%';

2. > 479 results
SELECT *
FROM `courses`
WHERE `cfu` > 10;

3. > 3468 results
SELECT *
FROM `students`
WHERE DATE_FORMAT(FROM_DAYS(DATEDIFF(NOW(), `date_of_birth`)), '%Y') + 0 > 30;

4. > 286 results
SELECT *
FROM `courses`
WHERE `period` = 'I semestre'
AND `year` = 1;

5. > 21 results
SELECT *
FROM `exams`
WHERE `date` = '2020-06-20'
AND time(`hour`) > '14:00:00';

6. > 38 results
SELECT *
FROM `degrees`
WHERE `level` = 'magistrale';

7. > 12 results
SELECT COUNT(*)
AS departmentsNumber
FROM `departments`;

8. > 50 results
SELECT COUNT(*)
AS teachersWithoutPhone
FROM `teachers`
WHERE `phone` IS NOT NULL;