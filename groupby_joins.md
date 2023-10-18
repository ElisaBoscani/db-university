Group by:
1 Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(\*) AS `total_student`, YEAR(`enrolment_date`) AS `year_registration` FROM `students` GROUP BY(`year_registration`);

////////

2 Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT `office_address`, COUNT(\*) AS `total_teachers` FROM`teachers` GROUP BY(`office_address`);

////////

3 Calcolare la media dei voti di ogni appello d'esame

SELECT `vote`, AVG(`vote`) AS `media_vote` FROM `exam_student` GROUP BY `vote`

////////

4 Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT `department_id`, COUNT(\*) AS `total_course` FROM `degrees` GROUP BY `department_id`;

///////
