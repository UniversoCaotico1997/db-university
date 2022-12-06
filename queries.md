Query Todo:

###########

1 Selezionare tutti gli studenti nati nel 1990 (160)

SELECT * 
FROM `students` 
WHERE year(date_of_birth) = 1990;

###########

2 Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT * 
FROM `courses` 
WHERE `cfu` > 10;

###########

3 Selezionare tutti gli studenti che hanno più di 30 anni

SELECT * 
FROM `students` 
WHERE TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE());

###########

4 Selezionare tutti i corsi del primo semestre del primo anno di un  qualsiasi corso di laurea (286)

SELECT * 
FROM `courses` 
WHERE `period` = 'I semestre' 
AND `year` = 1;

###########

5 Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

SELECT * 
FROM `exams`
WHERE date = '2020-06-20' 
AND `hour` >= '14:00:00';

########### 

6 Selezionare tutti i corsi di laurea magistrale (38)

SELECT * FROM `degrees` 
WHERE `level` = 'magistrale';

###########

7 Da quanti dipartimenti è composta l'università? (12)

SELECT COUNT(id) as departments 
FROM `departments`;

###########

8 Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT COUNT(id) as 'teachersphone' FROM `teachers` WHERE `phone` is Null;


###########

Group by:

###########

1 Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(id) AS total_student_of_year, Year(enrolment_date) AS year_enrolment_date 
FROM `students` 
GROUP BY year_enrolment_date;

###########

2 Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT COUNT(id) AS teachers_office_address, `office_address` FROM `teachers` 
GROUP BY office_address;

###########

3 Calcolare la media dei voti di ogni appello d'esame

SELECT exam_id AS average_marks, AVG(vote) 
FROM `exam_student` 
GROUP BY average_marks;

###########

4 Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT department_id AS total_department, COUNT(id) AS total_degree_courses 
FROM `degrees` 
GROUP BY total_department;

###########


Join:

###########

1 Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.`id`, `degrees`.`name` FROM `students` JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` WHERE `degrees`.`name` = 'Corso di Laurea in Economia'

###########

2 Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT `degrees`.`level`, `departments`.`name`
FROM `degrees`
JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id` 
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level`= 'Magistrale';

###########

3 Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT courses.* , `teachers`.`name`, `teachers`.`surname` 
FROM `course_teacher`  
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id` 
JOIN teachers ON `teachers`.`id` = `course_teacher`.`teacher_id` 
WHERE `teachers`.`id` = 44;

###########

4 Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.`name` AS student_name,`students`.`surname` AS student_surname, degrees.* , `departments`.`name` AS department_name 
FROM `degrees` 
JOIN `students` ON `degrees`.`id` = `students`.`degree_id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
ORDER BY `students`.`surname` ASC, `students`.`name` ASC;

###########

5 Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT degrees.*, `teachers`.`name` AS name_teacher, `teachers`.`surname` AS surname_teacher, `courses`.`name` AS name_course 
FROM `course_teacher` 
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` 
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`;

###########

6 Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT teachers.*, `departments`.`name` AS department_name 
FROM `course_teacher` 
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` 
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';

###########