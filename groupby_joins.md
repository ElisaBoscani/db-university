Group by:
1 Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(\*) AS `total_student`, YEAR(`enrolment_date`) AS `year_registration` FROM `students` GROUP BY(`year_registration`);

////////

2 Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT `office_address`, COUNT(\*) AS `total_teachers` FROM`teachers` GROUP BY(`office_address`);
