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

```

- 2 / Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
``` sql

```

- 3 / Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
``` sql

```

- 4 / Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
``` sql

```

- 5 / Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
``` sql

```

- 6 / Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
``` sql

```

- 7 / BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18
``` sql

```