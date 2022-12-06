Query Todo:

###########

1 Selezionare tutti gli studenti nati nel 1990 (160)

1 SELECT * FROM `students` WHERE year(date_of_birth) = 1990;

###########

2 Selezionare tutti i corsi che valgono più di 10 crediti (479)

2 SELECT * FROM `courses` WHERE `cfu` > 10;

###########

3 Selezionare tutti gli studenti che hanno più di 30 anni

3 SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE());

###########

4 Selezionare tutti i corsi del primo semestre del primo anno di un  qualsiasi corso di laurea (286)

4 SELECT * FROM `courses` WHERE `period` = 'I semestre' AND `year` = 1;

###########

5 Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

5 SELECT * FROM `exams` WHERE date = '2020-06-20' AND `hour` >= '14:00:00';

########### 

6 Selezionare tutti i corsi di laurea magistrale (38)

6 SELECT * FROM `degrees` WHERE `level` = 'magistrale';

###########

7 Da quanti dipartimenti è composta l'università? (12)

7 SELECT COUNT(id) as departments FROM `departments`;

###########

8 Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

8 SELECT COUNT(id) as 'teachersphone' FROM `teachers` WHERE `phone` is Null;


###########

Group by:

###########

1 Contare quanti iscritti ci sono stati ogni anno

1 SELECT COUNT(id) AS total_student_of_year, Year(enrolment_date) AS year_enrolment_date FROM `students` GROUP BY year_enrolment_date;

###########

2 Contare gli insegnanti che hanno l'ufficio nello stesso edificio


3 Calcolare la media dei voti di ogni appello d'esame



4 Contare quanti corsi di laurea ci sono per ogni dipartimento


###########


Join:
1 Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2 Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
3 Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4 Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
5 Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6 Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)