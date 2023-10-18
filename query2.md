##GROUP BY

- 1 / Contare quanti iscritti ci sono stati ogni anno
``` sql
SELECT COUNT(`students`.`id`) AS `students`, YEAR(`students`.`enrolment_date`) AS `year`
FROM `students`
GROUP BY `year`;
```

- 2 / Contare gli insegnanti che hanno l'ufficio nello stesso edificio
``` sql
SELECT COUNT(`teachers`.`id`) AS `teachers`, `teachers`.`office_address` AS `address`
FROM `teachers`
GROUP BY `address`
ORDER BY `teachers`;
```

- 3 / Calcolare la media dei voti di ogni appello d'esame
``` sql
SELECT AVG(`exam_student`.`vote`) AS voteAverage, `exam_student`.`exam_id` AS `examId`
FROM `exam_student`
GROUP BY `examId`;
```

- 4 / Contare quanti corsi di laurea ci sono per ogni dipartimento
``` sql
SELECT COUNT(`degrees`.`id`) AS `degrees`, `degrees`.`department_id` AS `departments`
FROM `degrees`
GROUP BY `departments`;
```


##JOIN
- 1 / Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
``` sql
SELECT `students`.`name` AS `Name`, `students`.`surname` AS `Surname`, `degrees`.`name` AS `Degree`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```

- 2 / Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
``` sql
SELECT `degrees`.`name` AS `Degree Name`, `degrees`.`level` AS `Level` ,`departments`.`name` AS `Department`
FROM `degrees`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `Level` = 'magistrale';
```

- 3 / Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
``` sql
SELECT `courses`.`name` AS `Course Name`, `teachers`.`id` AS `Teacher`
FROM `courses`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id` = 44;
```

- 4 / Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
``` sql
SELECT `students`.`surname` AS `Surname`, `students`.`name` AS `Name`, `degrees`.`name` AS `Degree`, `departments`.`name` AS `Department`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `Surname`, `Name`;
```

- 5 / Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
``` sql
SELECT `degrees`.`name` AS `Degree name`, `courses`.`name` AS `Course name`, `teachers`.`surname` AS `Teacher`
FROM `degrees`
JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY `Degree name`;
```

- 6 / Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
``` sql
SELECT DISTINCT `teachers`.`surname` AS `Surname`, `teachers`.`name` AS `Name`, `departments`.`name` AS `Department`
FROM `teachers`
JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
ORDER BY `Surname`;
```

- 7 / BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18
``` sql
SELECT `students`.`surname` AS `Surname`, `students`.`name` AS `Name`, `courses`.`name` AS `Exam`, COUNT(*) AS `Attempts`, MAX(`exam_student`.`vote`) AS `Max Vote`
FROM `students`
JOIN `exam_student`
ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams`
ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses`
ON `exams`.`course_id` = `courses`.`id`
WHERE `exam_student`.`vote` >= 18 -- voto minimo 18
GROUP BY `Surname`, `Name`, `Exam`
ORDER BY `Surname`, `Name`, `Exam`;
```