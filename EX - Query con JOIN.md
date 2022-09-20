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

SELECT `students`.`name`, `students`.`surname`, `degrees`.`name` as "nome_corso", `degrees`.`level` as "level_corso", `departments`.`name` as "nome_dipartimento"
FROM `students`
JOIN `degrees`ON `degrees`.`id` = `students`.`degree_id`
JOIN `departments`ON `departments`.`id` = `degrees`.`department_id`
ORDER BY `students`.`surname`, `students`.`name` ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT `exams`.`id` AS "id_corso_laurea", `courses`.`name` AS "nome_corso", `teachers`.`name`, `teachers`.`surname`
FROM `exams`
JOIN `courses` ON `courses`.`id` = `exams`.`course_id`
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT `teachers`.`name`,`teachers`.`surname`, `departments`.`name` 
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments`ON `departments`.`id`= `degrees`.`department_id`
WHERE `departments`.`name` = "Dipartimento di Matematica";


7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami

SELECT `students`.`name`, `courses`.`name`, COUNT(`exam_student`.`vote`) as 'nr_voti'
FROM `students`
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
JOIN `exam_student` ON `exam_student`.`student_id` = `students`.`id`
JOIN `exams` ON `exams`.`id` = `exam_student`.`exam_id`
JOIN `courses` ON `courses`.`id` = `exams`.`course_id`
GROUP BY `students`.`id`, `courses`.`id`;