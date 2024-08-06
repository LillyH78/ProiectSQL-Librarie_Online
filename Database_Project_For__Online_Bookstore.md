<h1>Database Project for **Online bookstore**</h1>

The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

Application under test: Online bookstore

Tools used: MySQL Workbench

Database description: 
The bookstore online has the purpose to sell books content on electronic format.
There are so many books categories such : Books for kids, Personal development, IT.
All the books are able to be ordered starting from Monday to saturday at every hour.
The orders placed on a non working day it will be processed in the first working day.


<ol>
<li>Database Schema </li>
<br>
You can find below the database schema that was generated through Reverse Engineer and which contains all the tables and the relationships between them.

The tables are connected in the following way:

<ul>
  <li> carti is connected with carti_comandate through a one to many relationship which was implemented through carti.id_carte as a primary key and carti_comandate.id_carte as a foreign key</li>
  <li> comenzi  is connected with carti_comandate through a one to many relationship which was implemented through comenzi.id_comanda as a primary key and carti_comandate.id_comanda as a foreign key</li>
  <li> clienti  is connected with comenzi_clienti through a one to many relationship which was implemented through clienti.id_client as a primary key and comenzi.clienti.id_client as a foreign key</li>
  <li> comenzi  is connected with comenzi_clienti through a one to many relationship which was implemented through comenzi.id_comanda as a primary key and comenzi_clienti.id_comanda as a foreign key</li>
  <li> plata  is connected with comenzi through a one to many relationship which was implemented through plata.id_modalitate_plata as a primary key and comenzi.tip_plata as a foreign key</li>
  <li> comenzi  is connected with livrare through a one to many relationship which was implemented through comenzi.id_comanda as a primary key and livrare.id_comanda as a foreign key</li>
</ul><br>

<li>Database Queries</li><br>

<ol type="a">
  
  <li>DDL (Data Definition Language)</li>

  The following instructions were written in the scope of CREATING the structure of the database (CREATE INSTRUCTIONS)
    
  CREATE DATABASE LIBRARIE_ONLINE;

  CREATE TABLE CARTI (
  ID_CARTE INT PRIMARY KEY AUTO_INCREMENT,
  DENUMIRE_CARTE VARCHAR (40),
  AUTOR VARCHAR (40),
  PRET INT,
  DATA_EDITIEI DATE
  );

  CREATE TABLE CLIENTI (
  ID_CLIENT INT PRIMARY KEY AUTO_INCREMENT,
  NUME VARCHAR (40),
  PRENUME VARCHAR (40),
  ADRESA VARCHAR (50),
  TELEFON VARCHAR (10)
  );

  CREATE TABLE COMENZI (
  ID_COMANDA INT NOT NULL AUTO_INCREMENT,
  COD_COMANDA VARCHAR (20),
  DATA_COMANDA DATE,
  PRIMARY KEY (ID_COMANDA)
  );

  CREATE TABLE CARTI_COMANDATE (
  ID_COMANDA INT,
  ID_CARTE INT,
  CANTITATE INT,
  foreign key (ID_COMANDA) references COMENZI (ID_COMANDA),
  foreign key (ID_CARTE) references CARTI(ID_CARTE)
  );
  
  CREATE TABLE COMENZI_CLIENTI (
  ID_COMANDA INT,
  ID_CLIENT INT,
  foreign key (ID_COMANDA) references COMENZI (ID_COMANDA),
  foreign key (ID_CLIENT) references CLIENTI(ID_CLIENT)
  );
  
  CREATE TABLE PLATA (
  ID_MODALITATE_PLATA INT PRIMARY KEY AUTO_INCREMENT,
  MODALITATE_PLATA VARCHAR(10)
  );

  CREATE TABLE LIVRARE (
  ID_LIVRARE INT NOT NULL AUTO_INCREMENT,
  MOD_LIVRARE VARCHAR(30),
  COST_TRANSPORT INT,
  ID_COMANDA INT,
  PRIMARY KEY (ID_LIVRARE),
  CONSTRAINT FK_LIVRARE_COMENZI
       FOREIGN KEY (ID_COMANDA) REFERENCES COMENZI(ID_COMANDA)
  );

  After the database and the tables have been created, a few ALTER instructions were written in order to update the structure of the database, as described below:

  # Modificare proprietate coloana MODALITATE_PLATA
  
  ALTER TABLE CARTI
  ADD COLUMN CATEGORII VARCHAR (20);

  # Adaugare coloana CATEGORII in tabela carti

  ALTER TABLE CARTI
  ADD COLUMN CATEGORII VARCHAR (20);

  # Stergere coloana CATEGORII din tabela carti
  
  ALTER TABLE CARTI
  DROP COLUMN CATEGORII;

  # Adaugare coloana COD_CARTE in tabela carti
  
  ALTER TABLE CARTI
  ADD COLUMN COD_CARTE VARCHAR (10) AFTER ID_CARTE;

  # Adaugare coloana CATEGORIE in tabela carti
  
  ALTER TABLE CARTI
  ADD COLUMN CATEGORIE VARCHAR (20) AFTER COD_CARTE;

  # Adaugare coloana ORAS in tabela CLIENTI
  
  ALTER TABLE CLIENTI
  ADD COLUMN ORAS VARCHAR (20) AFTER ADRESA;

  # Modificare proprietate coloana DATA_EDITIEI

  ALTER TABLE CARTI
  MODIFY DATA_EDITIEI VARCHAR (10);

  # Modificare denumire coloana

  ALTER TABLE CARTI CHANGE COLUMN DATA_EDITIEI AN_EDITIE VARCHAR(10);

  # Modificare proprietati coloane
  
  ALTER TABLE COMENZI
  MODIFY ID_COMANDA INT AUTO_INCREMENT;

  ALTER TABLE PLATA
  MODIFY MODALITATE_PLATA VARCHAR (20);

  ALTER TABLE CARTI
  MODIFY DATA_EDITIEI VARCHAR (10);
 
  <li>DML (Data Manipulation Language)</li>

  In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. 
  In the testing process, this necessary data is identified in the Test Design phase and created in the Test Implementation phase. 

  Below you can find all the insert instructions that were created in the scope of this project:

  # Adaugare date in tabela CARTI
  
  INSERT INTO CARTI (ID_CARTE, COD_CARTE, CATEGORIE, DENUMIRE_CARTE, AUTOR, PRET, AN_EDITIE)
  VALUES (1, 9335529  , 'Carti pentru copii', 'Dumbrava minunata', 'Mihail Sadoveanu', '25', '2020');

  INSERT INTO CARTI (ID_CARTE, COD_CARTE, CATEGORIE, DENUMIRE_CARTE, AUTOR, PRET, AN_EDITIE)
  VALUES (2, 7923391  , 'Carti pentru copii', 'Amintiri din copilarie', 'Ion Creanga', '17', '2011');

  INSERT INTO CARTI VALUES (3, 5712614, 'Carti pentru copii', 'Print si cersetor', 'Mark Twain', '10', '2014');

  # Modificare proprietate coloana DENUMIRE_CARTE

  ALTER TABLE CARTI
  MODIFY DENUMIRE_CARTE VARCHAR (100);

  INSERT INTO CARTI VALUES (4, 5712683, 'Carti pentru copii', 'Colt Alb', 'Jack London', '10', '2014'),
			   (5, 5715257, 'Carti pentru copii', 'Recreatia mare', 'Mircea Santimbreanu', '17', '2017'),
                           (6, 5715493, 'Carti pentru copii', 'Bunicul.Bunica', 'Barbu Stefanescu Delavrancea', '11', '2017'),
                           (7, 5713482, 'Carti pentru copii', 'Basme', 'Petre Ispirescu', '10', '2017'),
                           (8, 9345221, 'Carti pentru copii', 'Legendele olimpului', 'Alexandru Mitru', '25', '2022'),
                           (9, 7061680, 'Carti pentru copii', 'Din lumea celor care nu cuvanta', 'Emil Garleanu', '12', '2015'),
                           (10, 5712621, 'Carti pentru copii', 'Fram, ursul polar', 'Cezar Petrescu', '10', '2018'),
                           (11, 8852150, 'Dezvoltare personala', 'Cum sa comunici cu oricine', 'Leil Lowndes', '45', '2008'),
                           (12, 9456392, 'Dezvoltare personala', 'Arta manipularii', 'Kevin Dutton', '40', '2019'), 
                           (13, 4402547, 'Dezvoltare personala', 'Tata bogat, tata sarac', 'Robert T. Kiyosaki', '50', '2019'),
                           (14, 4400451, 'Dezvoltare personala', 'Atitudina este totul', 'Jeff Keller', '37', '2018'),
                           (15, 8998251, 'Dezvoltare personala', 'Gandeste si vei fi bogat', 'Napoleon Hill', '60', '2023'),
                           (16, 7891812, 'Dezvoltare personala', 'Gata cu scuzele', 'Rachel Hollis', '39', '2019'),
                           (17, 8814360, 'Dezvoltare personala', 'De vorba cu mine insumi', 'Prentice Mulford', '35', '2017'),
                           (18, 4404022, 'Dezvoltare personala', 'Abilitati de comunicare', 'Alan and Barbara Pease', '35', '2020'),
                           (19, 8852150, 'Dezvoltare personala', 'Arta manipularii', 'Kevin Dutton', '40', '2019'),
                           (20, 8859197, 'Dezvoltare personala', 'Cere si ti se va da', 'Ester and Jerry Hicks', '55', '2008'),
                           (21, 6559046, 'IT', 'Excel 2023.Curs pentru incepatori', 'Vlad Tudor', '30', '2023'), 
                           (22, 6559022, 'IT', 'Curs de programare in pyton 3', 'Vlad Tudor', '39', '2023'), 
                           (23, 6559121, 'IT', 'Word.Curs pentru incepatori', 'Vlad Tudor', '30', '2024'), 
                           (24, 2619039, 'IT', 'Proiectarea bazelor de date relationale cu Microsoft Access', 'Eugen Gabriel Garais', '44', '2024'), 
                           (25, 4684441, 'IT', 'Calculatorul in trei timpi', 'Mircea Badut', '38', '2021'), 
                           (26, 9417027, 'IT', 'Dezvoltarea rapida a aplicatiilor cu Visual Basic', 'Bazil Parv', '42', '2003'), 
                           (27, 6502439, 'IT', 'Instrumente web 2.0 utilizate in aplicatie', 'Traian Anghel', '36', '2008'), 
                           (28, 2600358, 'IT', 'Elemente de IT pentru administratia publica', 'Catalin Vrabie', '35', '2014'), 
                           (29, 3712159, 'IT', 'Conexiuni wireless cu Arduino', 'Mihai Todica', '46', '2021'), 
                           (30, 4624058, 'IT', 'Java de la 0 la expert', 'Stefan Tanasa', '149', '2011'); 

    # Adaugare date in tabela CLIENTI

    INSERT INTO CLIENTI (ID_CLIENT, NUME, PRENUME, ADRESA, ORAS, TELEFON)
    VALUES (1, 'Ionescu', 'Maria', 'Str. Rozelor nr 3, Sector 3', 'Bucuresti', '0722354789');

    INSERT INTO CLIENTI VALUES (2, 'Popescu', 'Ion', 'Aleea Trandafirilor, Sector 3', 'Bucuresti', '0732159357'),
			       (3, 'Popa', 'Stefan', ' Str I.C.Bratianu, nr 3', 'Pitesti', '0722369258'),
                               (4, 'Dumitrescu', 'Andrei', 'Str. Pandurilor nr 20', 'Pitesti', '0745789369'),
                               (5, 'Dragomir', 'Mihai', 'Str. 1 mai nr 7, Sector 1', 'Bucuresti', '0744589236'),
                               (6, 'Zamfiroiu', 'Alina', 'Str. 11 iunie', 'Bucuresti', '0745258369'),
                               (7, 'Badea', 'George', 'Str. Albatrosului, Sector 2', 'Bucuresti', '0745789456'),
                               (8, 'Erhan', 'Mihaela', 'Aleea Dealul Mitropoliei nr 9', 'Bucuresti', '0744521478'),
                               (9, 'Predescu', 'Gabriela', 'Str. I.C. Bratianu nr 3', 'Rm. Valcea', '0770258147'),
                               (10, 'Mihalache', 'Adina', 'Str. Mihail Sadoveanu, nr 12', 'Rm. Valcea', '0770741258'),
                               (11, 'Aleman', 'Rodica', 'Aleea Haiducului nr. 40', 'Rm. Valcea', '0722547821'),
                               (12, 'Apostolescu', 'Bogdan', 'Str. Alexe Ion, nr 37', 'Brasov', '0721546321'),
                               (13, 'Georgescu', 'Adriana', 'Str. Aleman nr 17', 'Brasov', '0723568974'),
                               (14, 'Parvulescu', 'Mihaela', 'Str. Rapsodiei nr 15', 'Brasov', '0766325748'),
                               (15, 'Dragomir', 'Marius', 'Aleea Rozelor nr 14', 'Pitesti', '0722535692');
 
  INSERT INTO CLIENTI (ID_CLIENT, NUME, PRENUME, ADRESA, ORAS, TELEFON)
  VALUES (16, 'Ionescu', 'Marius', 'Str. Rozelor nr 3, Sector 3', 'Bucuresti', '0722354789');

  INSERT INTO CLIENTI VALUES (17, 'Mojoiu', 'Dana', 'Str Panselutelor nr 23', 'Pitesti', '0741546789'),
			     (18, 'Olaru', 'Elisabeta', 'Aleea Florilor nr 15', 'Rm. Valcea', '0754654123'),
                             (19, 'Serban', 'Andreea', 'Str. Aurel Vlaicu nr 2', 'Bucuresti', '0722214785'),
                             (20, 'Popianu', 'Mihaela', 'Str. Aurel Vlaicu nr 9', 'Brasov', '0729335874');

  INSERT INTO CLIENTI VALUES (21, 'Zamfiroiu', 'Alina', 'Str. 11 iunie', 'Bucuresti', '0745258369', '6'),
                             (22, 'Badea', 'George', 'Str. Albatrosului, Sector 2', 'Bucuresti', '0745789456', '5'),
                             (23, 'Erhan', 'Mihaela', 'Aleea Dealul Mitropoliei nr 9', 'Bucuresti', '0744521478', '7'),
                             (24, 'Predescu', 'Gabriela', 'Str. I.C. Bratianu nr 3', 'Rm. Valcea', '0770258147', '7'),
                             (25, 'Mihalache', 'Adina', 'Str. Mihail Sadoveanu, nr 12', 'Rm. Valcea', '0770741258', '10'),
                             (26, 'Aleman', 'Rodica', 'Aleea Haiducului nr. 40', 'Rm. Valcea', '0722547821', '12'),
                             (27, 'Apostolescu', 'Bogdan', 'Str. Alexe Ion, nr 37', 'Brasov', '0721546321', '14'),
                             (28, 'Georgescu', 'Adriana', 'Str. Aleman nr 17', 'Brasov', '0723568974', '15'),
                             (29, 'Parvulescu', 'Mihaela', 'Str. Rapsodiei nr 15', 'Brasov', '0766325748', '16'),
                             (30, 'Popianu', 'Mihaela', 'Str. Aurel Vlaicu nr 9', 'Brasov', '0729335874', '15');

  # Modificare denumire coloana COD_COMANDA

  ALTER TABLE COMENZI CHANGE COLUMN COD_COMANDA NR_COMANDA VARCHAR(10);

  # Adaugare date in tabela COMENZI

  INSERT INTO COMENZI VALUES (1, '100', '2024-02-03'),
			     (2, '106', '2024-02-03'),
                             (3, '110', '2024-02-03'),
                             (4, '118', '2024-02-04'),
                             (5, '120', '2024-02-04'),
                             (6, '230', '2024-03-28'),
                             (7, '250', '2024-04-01'),
                             (8, '265', '2024-04-02'),
                             (9, '272', '2024-04-02'),
                             (10, '293', '2024-04-03'),
                             (11, '300', '2024-04-04'),
                             (12, '420', '2024-04-30'),
                             (13, '425', '2024-04-30'),
                             (14, '530', '2024-05-20'),
                             (15, '550', '2024-05-25'),
                             (16, '552', '2024-05-25'),
                             (18, '581', '2024-06-02'),
                             (19, '603', '2024-06-25'),
                             (20, '623', '2024-06-30');
   INSERT INTO COMENZI VALUES (21, '647', '2024-07-10');

   # Adaugare coloana TIP_PLATA in tabela comenzi

   ALTER TABLE COMENZI ADD COLUMN TIP_PLATA INT;
   ALTER TABLE COMENZI ADD foreign key(TIP_PLATA) references PLATA(ID_MODALITATE_PLATA);

   # Adaugare date in tabela CARTI_COMANDATE
   
   INSERT INTO CARTI_COMANDATE VALUES (1, 1, 1),
                                      (2, 1, 1), (2, 2, 1), (2, 3, 1),
                                      (3, 1, 1), (3, 2, 1), (3, 3, 1), (3, 4, 1),
                                      (4, 1, 1), (4, 2, 2), (4, 3, 1), (4, 4, 1),
                                      (5, 1, 2), (5, 2, 1), (5, 3, 1), (5, 4, 1), (5, 5, 2),
                                      (6, 1, 1), (6, 2, 1), (6, 3, 1), (6, 4, 1), (6, 5, 2),
                                      (7, 1, 1), (7, 2, 1), (7, 3, 2), (7, 4, 1), (7, 5, 2), (7, 6 ,1),
                                      (8, 1, 2), (8, 2, 1), (8, 3, 2), (8, 4, 1), (8, 5, 1), (8, 6, 1),
                                      (9, 1, 1), (9, 2, 1), (9, 3, 1), (9, 4, 1), (9, 5, 1), (9, 6, 1), (9, 7, 1),
                                      (10, 7, 1), (10, 8, 1), (10, 9, 1), (10, 10, 2), (10, 11, 1), (10, 12, 1),
                                      (11, 8, 1), (10, 9, 1), (10, 10, 1), (10, 11, 1), (10, 12, 1), (10, 13, 2),
                                      (12, 9, 1), (12, 10, 1), (12, 11, 2), (12, 12, 3), (12, 13, 1), (12, 14, 1),
                                      (13, 10, 1), (13, 11, 1), (13, 12, 1), (13, 13, 1), (13, 14, 1), (13, 15, 1),
                                      (14, 11, 1), (14, 12, 1), (14, 13, 1), (14, 14, 1), (14, 15, 1), (14, 16, 1),
                                      (15, 12, 1), (15, 13, 1), (15, 14, 1), (15, 15, 1), (15, 16, 1), (15, 17, 1);

    # Adaugare date in tabela COMENZI_CLIENTI 
    
    INSERT INTO COMENZI_CLIENTI VALUES (1, 1),
                                       (1, 2), (1, 3),
                                       (2, 1), (2, 2), (2, 3), (2, 4), (2, 5), (2, 6),
                                       (3, 6), (3, 7), (3, 8), (3, 9), (3, 10), (3, 11),
                                       (4, 7), (4, 8), (4, 9), (4, 10), (4, 11), (4, 12),
                                       (5, 8), (5, 9), (5, 10), (5, 11), (5, 12), (5, 13),
                                       (6, 9), (6, 10), (6, 11), (6, 12), (6, 13), (6, 14),
                                       (7, 10), (7, 11), (7, 12), (7, 13), (7, 14), (7, 15),
                                       (8, 10), (8, 11), (8, 12), (8, 13), (8, 14), (8, 15),
                                       (9, 1), (9, 2), (9, 3), (9, 4), (9, 5), (9, 6), (9, 7),
                                       (10, 2), (10, 3), (10, 4), (10, 5), (10, 6), (10, 7), (10, 8),
                                       (11, 3), (11, 4), (11, 5), (11, 6), (11, 7), (11, 8), (11, 9),
                                       (12, 4), (12, 5), (12, 6), (12, 7), (12, 8), (12, 9), (12, 10),
                                       (13, 5), (13, 6), (13, 7), (13, 8), (13, 9), (13, 10), (13, 11),
                                       (14, 6), (14, 7), (14, 8), (14, 9), (14, 10), (14, 11), (14, 12),
                                       (15, 7), (15, 8), (15, 9), (15, 10), (15, 11), (15, 12), (15, 13);

    # Adaugare date in tabela LIVRARE

    INSERT INTO LIVRARE VALUES (1, 'CURIER', '20', '1'),
                               (2, 'EASYBOX', '0', '2'),
                               (3, 'MAGAZIN', '0', '3'),
                               (4, 'MAGAZIN', '0', '4'),
                               (5, 'MADAZIN', '0', '5'),
                               (6, 'CURIER', '20', '6'),
                               (7, 'CURIER', '25', '7'),
                               (8, 'CURIER', '25', '8'),
                               (9, 'EASYBOX', '0', '9'),
                               (10, 'EASYBOX', '0', '10'),
                               (11, 'EASYBOX', '0', '11'),
                               (12, 'EASYBOX', '0', '12'),
                               (13, 'MAGAZIN', '0', '13'),
                               (14, 'CURIER', '25', '14'),
                               (15, 'CURIER', '25', '15');

   # Adaugare date in tabela PLATA
   INSERT INTO PLATA VALUES (1,'Cash'), (2, 'Card');
   
   INSERT INTO PLATA (MODALITATE_PLATA) VALUES ('Cash'), ('Card');
   INSERT INTO PLATA (MODALITATE_PLATA) VALUES ('Card cadou');
       
   After the insert, in order to prepare the data to be better suited for the testing process, I updated some data in the following way:  
  
   UPDATE CARTI
   SET PRET='40'
   WHERE ID_CARTE=14;
   
   UPDATE CARTI_COMANDATE
   SET CANTITATE='2'
   WHERE ID_COMANDA=2 AND ID_CARTE=3;

   UPDATE CLIENTI
   SET NUME='MIRON'
   WHERE ID_CLIENT=15;

   UPDATE COMENZI
   SET ID_COMANDA='17'
   WHERE ID_COMANDA=18; 

   UPDATE COMENZI
   SET ID_COMANDA='18'
   WHERE ID_COMANDA=19;

   UPDATE COMENZI
   SET ID_COMANDA='19'
   WHERE ID_COMANDA=20;

   UPDATE COMENZI
   SET TIP_PLATA = 1
   WHERE ID_COMANDA <=10;   

   UPDATE COMENZI
   SET TIP_PLATA = 2
   WHERE ID_COMANDA >10;  

  <li>DQL (Data Query Language)</li>

 After the testing process, I deleted the data that was no longer relevant in order to preserve the database clean: 

  SET SQL_SAFE_UPDATES=0;
  DELETE FROM CARTI;

  DELETE FROM CLIENTI
  WHERE ID_CLIENT='16';

  In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:

  # Selectarea tabelelor
  
  SELECT * FROM CARTI;  
  SELECT * FROM CLIENTI;
  
  # Selectarea unor coloane din tabel
  
  SELECT ID_CARTE, CATEGORIE, DENUMIRE_CARTE FROM CARTI;

  # Returnarea clientilor care locuiesc in Bucuresti
  
  SELECT * FROM CLIENTI
  WHERE ORAS='BUCURESTI';
  
  # Returnarea cartilor cu pretul mai mare de 20

  SELECT * FROM CARTI 
  WHERE PRET>20;

  # Returnarea cartilor care au in denumire "bogat"
  
  SELECT * FROM CARTI
  WHERE DENUMIRE_CARTE LIKE '%BOGAT%';

  # Returnarea cartilor al caror pret incepe cu 1, este partial cunoscut si sunt editate in 2017
  
  SELECT * FROM CARTI
  WHERE PRET LIKE '1_' AND AN_EDITIE LIKE '%2017%';

  # Returnarea cartilor al caror pret incepe cu 1, este partial cunoscut sau sunt editate in 2017 

  SELECT * FROM CARTI
  WHERE PRET LIKE '1_' OR AN_EDITIE LIKE '%2017%';

  # Returnarea cartilor al caror pret incepe cu 1, este partial cunoscut si sunt editate in 2017 sau in 2018

  SELECT * FROM CARTI
  WHERE PRET LIKE '1_' 
  AND (AN_EDITIE = '2017'
		OR AN_EDITIE = '2018');
  
  # Returnarea cartilor a caror denumire nu incepe cu "C"
  
  SELECT * FROM CARTI
  WHERE DENUMIRE_CARTE NOT LIKE 'C%';

  # Returnarea cartilor a caror denumire incepe cu "C" ordonate descrescator
  
  SELECT * FROM CARTI
  WHERE DENUMIRE_CARTE LIKE 'C%'
  ORDER BY COD_CARTE DESC;
  
  # Returnarea cartilor din categoria IT, ordonate descrescator cu limita 5 
  
  SELECT * FROM CARTI 
  WHERE CATEGORIE LIKE 'IT'
  ORDER BY COD_CARTE DESC
  LIMIT 5;

  # Returnarea pretului maxim al cartilor
  SELECT MAX(PRET)
  FROM CARTI;

  # Returnarea pretului minim al cartilor

  SELECT MIN(PRET)
  FROM CARTI;

  # Returnarea ultimei comenzi facuta de Zamfiroiu Alina

  SELECT CLIENTI.NUME, CLIENTI.PRENUME, MIN(DATA_COMANDA)
  FROM CLIENTI
  JOIN COMENZI ON COMENZI.ID_COMANDA = CLIENTI.ID_COMANDA
  WHERE Nume = 'Zamfiroiu'
  AND Prenume = 'Alina';

  # Returnarea comenzilor facute de Zamfiroiu Alina

  SELECT CLIENTI.NUME, CLIENTI.PRENUME, COMENZI.ID_COMANDA, COMENZI.DATA_COMANDA
  FROM CLIENTI
  JOIN COMENZI_CLIENTI ON CLIENTI.ID_CLIENT = COMENZI_CLIENTI.ID_CLIENT
  JOIN COMENZI ON COMENZI_CLIENTI.ID_COMANDA = COMENZI.ID_COMANDA
  WHERE Nume = 'Zamfiroiu'
  AND Prenume = 'Alina';

  # Returnarea numarului total de carti din librarie

  SELECT COUNT(*)
  FROM CARTI;

  # Returnarea mediei de pret a cartilor vandute

  SELECT AVG(PRET)
  FROM CARTI;

  # Returnarea pretului mediu pt produsele din categoria IT si Dezvoltare personala

  SELECT CATEGORIE, AVG(PRET)
  FROM CARTI 
  GROUP BY CATEGORIE;

  # Returnarea cartilor din categoria IT care au media pretului sub 50

  SELECT CATEGORIE, AVG(PRET)
  FROM CARTI 
  WHERE CATEGORIE='IT'
  GROUP BY CATEGORIE
  HAVING AVG(PRET) < 50;

  # Returnarea cartilor pe fiecare client

  SELECT CLIENTI.ID_CLIENT, NUME, PRENUME, COUNT(ID_CARTE) 
  FROM CLIENTI 
  JOIN COMENZI_CLIENTI ON COMENZI_CLIENTI.ID_CLIENT = CLIENTI.ID_CLIENT
  JOIN CARTI_COMANDATE ON COMENZI_CLIENTI.ID_COMANDA = CARTI_COMANDATE.ID_COMANDA
  GROUP BY CLIENTI.ID_CLIENT, NUME, PRENUME
  HAVING COUNT(ID_CARTE) > 5;

  # Returnarea nr de clienti din fiecare oras (doar orasele care contin mai mult de 2 clienti)

  SELECT COUNT(ID_CLIENT), ORAS
  FROM CLIENTI
  GROUP BY ORAS
  HAVING COUNT(ID_CLIENT) > 2
  ORDER BY COUNT(ID_CLIENT) ASC;
  
  # Returnarea tuturor cartilor comandate 
  SELECT * FROM CARTI C 
  JOIN CARTI_COMANDATE CC ON C.ID_CARTE = CC.ID_COMANDA;

  # Returnarea cartilor comandate si livrate
  SELECT C.COD_CARTE, C.DENUMIRE_CARTE, L.MOD_LIVRARE
  FROM CARTI C 
  JOIN CARTI_COMANDATE CC ON CC.ID_CARTE = C.ID_CARTE
  JOIN LIVRARE L ON L.ID_COMANDA = CC.ID_COMANDA;

  # Returnarea tuturor cartilor care au fost comandate cat si a celor care nu au fost comandate

  SELECT * FROM CARTI C 
  LEFT JOIN CARTI_COMANDATE CC ON C.ID_CARTE = CC.ID_CARTE;

  SELECT * FROM CARTI_COMANDATE CC
  RIGHT JOIN CARTI C ON CC.ID_CARTE = C.ID_CARTE;

  SELECT * FROM COMENZI C 
  RIGHT JOIN LIVRARE L ON L.ID_COMANDA = C.ID_COMANDA;

  SELECT * FROM CARTI C 
  CROSS JOIN CARTI_COMANDATE CC ON C.ID_CARTE = CC.ID_CARTE;

  # Returnarea nr de carti comandate pt fiecare autor
  SELECT C.AUTOR, COUNT(*)
  FROM CARTI_COMANDATE CC
  INNER JOIN CARTI C ON CC.ID_CARTE = C.ID_CARTE
  GROUP BY C.AUTOR;

  # Returnarea tuturor comenzilor platite prin cash

  SELECT * FROM COMENZI
  WHERE TIP_PLATA = (SELECT ID_MODALITATE_PLATA
						FROM PLATA
						WHERE MODALITATE_PLATA = 'Cash');

  # Returnarea tuturor comenzilor platite prin Cash si Card
                
  SELECT * FROM COMENZI
  where tip_plata IN (SELECT ID_MODALITATE_PLATA
					FROM PLATA
					WHERE MODALITATE_PLATA in ('Cash','Card'));

     
</ol>

<li>Conclusions</li>



</ol>
