Group by:
1 Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(\*) AS `total_student`, YEAR(`enrolment_date`) AS `year_registration` FROM `students` GROUP BY(`year_registration`);

////////
