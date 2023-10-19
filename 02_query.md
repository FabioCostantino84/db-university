# Group by:
- 1. Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT YEAR(`enrolment_date`) AS `enrolment_year`,
    count(*) AS `enrolment_total`
    FROM `students`
    GROUP BY year(`enrolment_date`) 
    ORDER BY `enrolment_year` DESC;
```
- 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT `office_address`,     
     count(*) AS `total_teachers`
     FROM `teachers`
     GROUP BY `office_address` 
     ORDER BY `total_teachers` ASC;
```
- 3. Calcolare la media dei voti di ogni appello d'esame
```sql
SELECT `exam_id`, avg(`vote`) AS `average_rating`
    -> FROM `exam_student`
    -> GROUP BY `exam_id`;
```
- 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
SELECT `department_id`, count(*) AS `total_degrees_dep`
    -> FROM `degrees`
    -> GROUP BY `department_id`;
```
# Joins:
- 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```sql
SELECT `students`.*
     FROM `students`
     JOIN `degrees` ON `degree_id` = `degrees`.`id`                 
     WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```
- 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscien
```sql
SELECT `degrees`.`name` , `degrees`.`level` , `departments`.`name` AS `department_name`
     FROM `degrees`
     JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
     WHERE `degrees`.`name` LIKE 'Corso di Laurea Magistrale%'
     AND `departments`.`name` = 'Dipartimento di Neuroscienze';
```
- 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
SELECT `courses`.`name` , `courses`.`description` , `course_teacher`.`teacher_id` 
FROM `courses` 
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id` 
WHERE `course_teacher`.`teacher_id` = 44;

```
- 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```sql

```
- 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql

```
- 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
```sql
SELECT DISTINCT `teachers`.`id`, `teachers`.`name`, `teachers`.`surname` 
FROM `teachers`
JOIN `course_teachers` ON  `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course`.`id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`id` = 5;
```
# BONUS: 
- 7. Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
```sql
SELECT `students`.`id`, `students`.`name`, `students`.`surname`, `courses`.`name`, 
COUNT(`exam_student`.`vote`) AS `number_test`, 
MAX(`exam_student`.`vote`) AS `max_vote`
FROM `students`
JOIN `exam_student` ON `students`.`id` = `axam_student`.`student_id`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
GROUP BY `students`.`id`, `courses`.`id`
HAVING `max_vote` >= 18;
```