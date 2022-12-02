Modellizzare la struttura di una tabella per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

dipartimenti
- id PK AI UN NN 
- nome | VARCHAR(60) NN
- descrizione | TEXT NULL

studente 
- id PK AI UN NN 
- corsi_ID | FK BIGINT
- nome | VARCHAR(20) NN
- cognome | VARCHAR(20) NN
- email | VARCHAR(30) NULL
- numero | VARCHAR(15) NULL
- matricola| VARCHAR(10) NN
- corso_laurea_id | BIGINT

corsi
- id PK AI UN NN 
- ore_lezioni | SMALLINT | NN 
- docente_id | FK BIGINT NULL 
- aula | VARCHAR(5) NULL
- nome | VARCHAR(30) NN
- programma | TEXT NN
- modalità_frequenza | VARCHAR(20) NULL

corsi_di_Laurea
- id PK AI UN NN 
- corso_id | FK BIGINT
- programma | TEXT NN
- durata | VARCHAR(10) NULL
- data_inizio | DATE NN
- sede | VARCHAR(20) NN
- dipartimento_id | FK BIGINT
- lingua |VARCHAR(20) NN


insegnanti 
- id PK AI UN NN 
- nome | VARCHAR(20) NN
- cognome | VARCHAR(20) NN
- corso_id | FK BIGINT

appelli
- id PK AI UN NN 
- corso_id | FK BIGINT
- aula | VARCHAR(5) NULL
- nome | VARCHAR(20) NN
- data | DATE NN
- tipologia | VARCHAR(20) NN


appelli_studenti(pvot)
- voto | DECIMAL(3,1) NULL
- appello_id |
- studente_id |


corsi_insegnanti(pvot)
- isegnanti_id
- corso_id


######
relazioni



OneToManY => dipartimento & corsi_di_laurea
OneToMany => corsi_di_laurea & corsi 
ManyToMany => corsi & insegnanti(pvot) 
ManyToMany => appelli & studente(pvot)
OneToMany  => corso & studente 
ManyToMany => appelli & corsi 







