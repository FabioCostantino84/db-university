# Group by:
- 1. Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT YEAR(enrolment_date) AS enrolment_year,
    count(*) AS enrolment_total
    FROM students
    GROUP BY year(enrolment_date) 
    ORDER BY enrolment_year DESC;
```
- 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
select office_address,     
     count(*) as total_teachers
     from teachers
     group by office_address 
     order by total_teachers asc;
```
- 3. Calcolare la media dei voti di ogni appello d'esame
```sql
select exam_id, avg(vote) as average_rating
    -> from exam_student
    -> group by exam_id;
```
- 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
select department_id, count(*) as total_degrees_dep
    -> from degrees
    -> group by department_id;
```
# Joins:
- 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
- 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
- 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
- 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
- 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
- 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
# BONUS: 
- 7. Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.