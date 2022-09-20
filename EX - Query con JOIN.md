1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `degrees`.`name`, `students`.`name`, `students`.`surname` 
FROM `degrees` 
JOIN `students` 
ON `students`.`degree_id` = `degrees`.`id` 
WHERE `degrees`.`name` = "Corso di Laurea in Economia";

2. Selezionare tutti i Corsi di Laurea del Dipartimento di Neuroscienze

SELECT `departments`.`name`, `degrees`.`name` 
FROM `degrees` 
JOIN `departments` 
ON `departments`.`id` = `degrees`.`department_id` 
WHERE `departments`.`name` = "Dipartimento di Neuroscienze"; 

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `teachers`.`name`, `teachers`.`surname`, `courses`.`name` as "nome_corso", `courses`.`id` as "id_corso" 
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
WHERE `teachers`.`name` = "Fulvio"
AND `teachers`.`surname` = "Amato";

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami