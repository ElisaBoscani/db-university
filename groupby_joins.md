Group by:
1 Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(\*) AS `total_student`, YEAR(`enrolment_date`) AS `year_registration` FROM `students` GROUP BY(`year_registration`);

////////

2 Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT COUNT(\*) AS `total_teachers`, `office_address` FROM`teachers` GROUP BY(`office_address`);

////////

3 Calcolare la media dei voti di ogni appello d'esame

SELECT AVG(`vote`) AS `media_vote`, `vote` FROM `exam_student` GROUP BY `vote`

////////

4 Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT COUNT(\*) AS `total_course`, `department_id` FROM `degrees` GROUP BY `department_id`;

///////
JOIN

1 Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.\* FROM `students` JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` WHERE `degrees`.`name` = "Corso di Laurea in Economia";

/////////

2 Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT `degrees`.\* FROM `degrees` JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` WHERE `departments`.`name` = "Dipartimento di Neuroscienze" AND `degrees`.`level`="magistrale";

///////

3 Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`._, `teachers`._ FROM `course_teacher` JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id`= 44 AND `teachers`.`name`= "fulvio";

///////

4 Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.`surname`, `students`.`name`, `degrees`.`name` AS `degrees_name`, `departments`.`name` AS `departments_name` FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`

/////////

5 Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT `degrees`.`name` AS `degrees_name`, `teachers`.`name` AS `teachers_name`, `teachers`.`surname`, `courses`.`name` AS `courses_name` FROM `courses`
JOIN `degrees`ON `courses`.`degree_id` = `degrees`.`id`
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY `degrees`.`name`

//////////////

6 Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT `teachers`.\* FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` ="Dipartimento di Matematica"

//////
7 Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo.

SELECT `students`.`name` AS `student_name`, `students`.`surname` , `exams`.`course_id`, COUNT(`exam_student`.`vote`) AS `numero_tentativi` , MAX(`exam_student`.`vote`) AS `voto_max` FROM `students` JOIN `exam_student` ON `students`.`id` =`exam_student`.`student_id` JOIN `exams` ON `exam_student`.`exam_id`=`exams`.`id` GROUP BY `students`.`name`, `students`.`surname`, `exams`.`course_id`;

Successivamente, filtrare i tentativi con voto minimo 18.
SELECT `students`.`name` AS `student_name`, `students`.`surname` , `exams`.`course_id`, COUNT(`exam_student`.`vote`) AS `numero_tentativi` , MIN(`exam_student`.`vote`) AS `voto_min` FROM `students` JOIN `exam_student` ON `students`.`id` =`exam_student`.`student_id` JOIN `exams` ON `exam_student`.`exam_id`=`exams`.`id` GROUP BY `students`.`name`, `students`.`surname`, `exams`.`course_id` HAVING `voto_min` >=18;
