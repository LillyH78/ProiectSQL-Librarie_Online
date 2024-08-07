## Database Project for **Online bookstore**
The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

Application under test: Online bookstore

Tools used: MySQL Workbench

Database description: The bookstore online has the purpose to sell books content on electronic format. There are so many books categories such : Books for kids, Personal development, IT. All the books are able to be ordered starting from Monday to saturday at every hour. The orders placed on a non working day it will be processed in the first working day.

   1. Database Schema 

      You can find below the database schema that was generated through Reverse Engineer and which contains all the tables and the relationships between them.


      The tables are connected in the following way:

      * **carti** is connected with carti_comandate through a **one to many** relationship which was implemented through **carti.id_carte** as a primary key and **carti_comandate.id_carte** as a foreign key
      * **comenzi**  is connected with **carti_comandate** through a **one to many** relationship which was implemented through **comenzi.id_comanda** as a primary key and **carti_comandate.id_comanda** as a foreign key
      * **clienti**  is connected with **comenzi_clienti** through a **one to many** relationship which was implemented through **clienti.id_client** as a primary key and **comenzi.clienti.id_client** as a foreign key
      * **comenzi**  is connected with **comenzi_clienti** through a **one to many** relationship which was implemented through **comenzi.id_comanda** as a primary key and **comenzi_clienti.id_comanda** as a foreign key
      * **plata**  is connected with **comenzi** through a **one to many** relationship which was implemented through **plata.id_modalitate_plata** as a primary key and comenzi.tip_plata as a foreign key
      * **comenzi**  is connected with **livrare** through a **one to many** relationship which was implemented through **comenzi.id_comanda** as a primary key and **livrare.id_comanda** as a foreign key

   2. Database Queries
  
      i. DDL (Data Definition Language)

         The following instructions were written in the scope of CREATING the structure of the database (CREATE INSTRUCTIONS)
    
      * create database librarie_online;
      * create table carti(
        id_carte int primary key auto_increment,
        denumire_carte varchar (40),
        autor varchar (40),
        pret int,
        data_editiei date
        );

      * create table clienti(
        id_client int primary key auto_increment,
        nume varchar (40),
        prenume varchar (40),
        adresa varchar (50),
        telefon varchar(10)
        );
    
      * create table comenzi(
        id_comanda int not null auto_increment
        cod_comanda varhar (20),
        data_comanda date,
        primary key (id_comanda)
        );

      * create table carti_comandate(
        id_comanda int,
        id_carte int,
        cantitate int
        foreign key (id_comanda) references comenzi (id_comanda),
        foreign key (id_carte) references carti(id_carte)
        );
  
      * create table comenzi_clienti(
        id_comanda int,
        id_client int,
        foreign key (id_comanda) references comenzi (id_comanda),
        foreign key (id_client) references clienti(id_client)
        );
  
      * create table plata(
        id_modalitate_plata int primary key auto_increment,
        modalitate_plata varchar(10)
        );
  
      * create table livrare(
        id_livrare int not null auto_increment,
        mod_livrare varchar(30),
        cost_transport int,
        id_comanda int,
        primary key (id_livrare),
        constraint fk_livrare_comenzi
             foreign key (id_comanda) references comenzi(id_comanda)
        );
  
      After the database and the tables have been created, a few ALTER instructions were written in order to update the structure of the database, as described below:

      * Adaugare coloana categorii in tabela carti

           * alter table carti
           add column categorii varchar (20);

      * Stergere coloana categorii din tabela carti
  
           * alter table carti
           drop column categorii;

      * Adaugare coloana cod_carte in tabela carti
  
           * alter table carti
           add column cod_carte varchar (10) after id_carte;

      * Adaugare coloana categorie in tabela carti
  
           * alter table carti
           add column categorie varchar (20) after cod_carte;

      * Adaugare coloana oras in tabela clienti
  
           * alter table clienti
           add column oras varchar (20) after adresa;

      * Modificare proprietate coloana data_editiei

           * alter table carti
           modify data_editiei varchar (10);

      * Modificare denumire coloana

           * alter table carti change column data_editiei an_editie varchar (10);

      * Modificare proprietati coloane
  
           * alter table comenzi
           modify id_comanda int auto_increment;

           * alter table plata
           modify modalitate_plata varchar (20);

           * alter table carti
           modify data_editiei varchar (10);
 
       ii. DML (Data Manipulation Language)
        In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. In the testing process, this necessary data is identified in the Test Design phase and created in the Test Implementation phase. 

        Below you can find all the insert instructions that were created in the scope of this project:

        * Adaugare date in tabela CARTI
  
          * insert into carti (id_carte, cod_carte, categorie, denumire_carte, autor, pret, an_editie) 
          values (1, 9335529  , 'Carti pentru copii', 'Dumbrava minunata', 'Mihail Sadoveanu', '25', '2020');

          * insert into carti (id_carte, cod_carte, categorie, denumire_carte, autor, pret, an_editie)
          values (2, 7923391  , 'Carti pentru copii', 'Amintiri din copilarie', 'Ion Creanga', '17', '2011');

          * insert into carti (3, 5712614, 'Carti pentru copii', 'Print si cersetor', 'Mark Twain', '10', '2014');

        * Modificare proprietate coloana DENUMIRE_CARTE

          alter table carti
          modify denumire_carte varchar (100);

          * insert into carti values (4, 5712683, 'Carti pentru copii', 'Colt Alb', 'Jack London', '10', '2014'),
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

        * Adaugare date in tabela CLIENTI

          * insert into clienti (id_client, nume, prenume, adresa, oras, telefon)
            values (1, 'Ionescu', 'Maria', 'Str. Rozelor nr 3, Sector 3', 'Bucuresti', '0722354789');

          * insert into clienti values (2, 'Popescu', 'Ion', 'Aleea Trandafirilor, Sector 3', 'Bucuresti', '0732159357'),
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
 
          * insert into clienti (ID_CLIENT, NUME, PRENUME, ADRESA, ORAS, TELEFON)
            values (16, 'Ionescu', 'Marius', 'Str. Rozelor nr 3, Sector 3', 'Bucuresti', '0722354789');

          * insert into clienti values (17, 'Mojoiu', 'Dana', 'Str Panselutelor nr 23', 'Pitesti', '0741546789'),
			     (18, 'Olaru', 'Elisabeta', 'Aleea Florilor nr 15', 'Rm. Valcea', '0754654123'),
                             (19, 'Serban', 'Andreea', 'Str. Aurel Vlaicu nr 2', 'Bucuresti', '0722214785'),
                             (20, 'Popianu', 'Mihaela', 'Str. Aurel Vlaicu nr 9', 'Brasov', '0729335874');

          * insert into clienti values (21, 'Zamfiroiu', 'Alina', 'Str. 11 iunie', 'Bucuresti', '0745258369', '6'),
                             (22, 'Badea', 'George', 'Str. Albatrosului, Sector 2', 'Bucuresti', '0745789456', '5'),
                             (23, 'Erhan', 'Mihaela', 'Aleea Dealul Mitropoliei nr 9', 'Bucuresti', '0744521478', '7'),
                             (24, 'Predescu', 'Gabriela', 'Str. I.C. Bratianu nr 3', 'Rm. Valcea', '0770258147', '7'),
                             (25, 'Mihalache', 'Adina', 'Str. Mihail Sadoveanu, nr 12', 'Rm. Valcea', '0770741258', '10'),
                             (26, 'Aleman', 'Rodica', 'Aleea Haiducului nr. 40', 'Rm. Valcea', '0722547821', '12'),
                             (27, 'Apostolescu', 'Bogdan', 'Str. Alexe Ion, nr 37', 'Brasov', '0721546321', '14'),
                             (28, 'Georgescu', 'Adriana', 'Str. Aleman nr 17', 'Brasov', '0723568974', '15'),
                             (29, 'Parvulescu', 'Mihaela', 'Str. Rapsodiei nr 15', 'Brasov', '0766325748', '16'),
                             (30, 'Popianu', 'Mihaela', 'Str. Aurel Vlaicu nr 9', 'Brasov', '0729335874', '15');

        * Modificare denumire coloana cod_comanda

          alter table comenzi change column cod_comanda nr_comanda varchar (10);

        * Adaugare date in tabela comenzi

          * insert into comenzi values (1, '100', '2024-02-03'),
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
          * insert into comenzi values (21, '647', '2024-07-10');

         * Adaugare coloana tip_plata in tabela comenzi

           alter table comenzi add column tip_plata int;
           alter table comenzi add foreign key(tip_plata) references plata(id_modalitate_plata);

         * Adaugare date in tabela carti_comandate
   
           * insert into carti_comandate values (1, 1, 1),
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

         * Adaugare date in tabela comenzi_clienti 
    
           * insert into comenzi_clienti values (1, 1),
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

         * Adaugare date in tabela livrare

           * insert into livrare values (1, 'CURIER', '20', '1'),
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

         * Adaugare date in tabela plata    
            * insert into plata values (1,'Cash'), (2, 'Card');
   
            * insert into plata (modalitate_plata) values ('Cash'), ('Card');
            * insert into plata (modalitate_plata) values ('Card cadou');
       
         After the insert, in order to prepare the data to be better suited for the testing process, I updated some data in the following way:  
  
       * update carti
         set pret='40'
         where id_carte=14;
   
       * update carti_comandate
         set cantitate='2'
         where id_comanda=2 and id_carte=3;

       * update clienti
         set nume='MIRON'
         where id_client=15;

       * update comenzi
         set id_comanda='17'
         where id_comanda=18; 

       * update comenzi
         set id_comanda='18'
         where id_comanda=19;

       * update comenzi
         set id_comanda='19'
         where id_comanda=20;

       * update comenzi
         set tip_plata = 1
         where id_comanda <=10;   

       * update comenzi
         set tip_plata = 2
         where id_comanda >10;  

      After the testing process, I deleted the data that was no longer relevant in order to preserve the database clean: 

       * set sql_safe_updates=0;
         delete from carti;

       * delete from carti
         where id_client='16';

       iii. DQL (Data Query Language) 
         In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:

         * Return all data from the books and customers tables
  
            ```sql
            select * from carti;  
            select * from clienti;
            ```
            
        * Return book_id, category and book_name from books table
            
            ```sql
            select id_carte, categorie, denumire_carte from carti;
            ```
            
        * Return customers who live in Bucharest
            
            ```sql
            select * from clienti
            where oras='bucuresti';
            ```
            
        * Return books with a price higher than 20
        
            ```sql
            select * from carti 
            where pret>20;
            ```

        * Return books that have "rich" in their name

            ```sql
            select * from carti
            where denumire_carte like '%bogat%';
            ```

        * Return books whose price starts with 1, is partially known and they are published in 2017
            
            ```sql
            select * from carti
            where pret like '1_' and an_editie like '%2017%';
            ```

        * Return books whose price starts with 1, is partially known or they are published in 2017
        
            ```sql            
            select * from carti 
            where pret like '1_' or an_editie like '%2017%';
            ```

        * Return books whose price starts with 1, is partially known and they are published in 2017 or 2018
        
            ```sql
            select * from carti
            where pret like '1_' 
            and (an_editie = '2017'
		   or an_editie = '2018');
            ```
  
        * Returning books whose name does not begin with "C"
      
            ```sql
            select * from carti
            where denumire_carte not like 'C%';
            ```

        * Returning books whose name starts with "C" in descending order 

            ```sql
            select * from carti
            where denumire_carte like 'C%' 
            order by cod_carte desc;
            ```
  
        * Returning books from the IT category, sorted in descending order with a limit of 5

            ```sql
            select * from carti 
            where categorie like 'IT' 
            order by cod_carte desc
            limit 5;
            ```

        * Returning the maximum price of the books

            ```sql
            select max(pret)
            from carti;
            ```

        * Returning the minimum price of the books

            ```sql
            select min(pret)
            from carti;
            ```

        * The return of the last order made by Zamfiroiu Alina

            ```sql        
            select clienti.nume, clienti.prenume, min(data_comanda)
            from clienti
            join comenzi on comenzi.id_comanda = clienti.id_comanda
            where nume = 'zamfiroiu'
            and prenume = 'alina';
            ```

        * The return of all orders made by Zamfiroiu Alina

            ```sql
            select clienti.nume, clienti.prenume, comenzi.id_comanda, comenzi.data_comanda
            from clienti
            join comenzi_clienti on clienti.id_client = comenzi_clienti.id_client
            join comenzi on comenzi_clienti.id_comanda = comenzi.id_comanda
            where nume = 'zamfiroiu'
            and prenume = 'alina';
            ```	    

        * Returning the total number of books in the library

            ```sql
            select count(*)
            from carti;
            ```

        * Returning the average price of the books sold

            ```sql
            select AVG(pret)
            from carti;
            ```

        * Return of the average price for products in the IT and Personal Development category

            ```sql            
            select categorie, avg(pret) 
            from carti 
            group by categorie;
            ```

        * Returning books from the IT category that have an average price below 50

            ```sql
            select categorie, avg(pret)
            from carti 
            where categorie='it'
            group by categorie
            having avg(pret) < 50;
            ```	    

        * Returning books for each customer

            ```sql
            select clienti.id_client, nume, prenume, count(id_carte) 
            from clienti 
            join comenzi_clienti on comenzi_clienti.id_client = clienti.id_client
            join carti_comandate on comenzi_clienti.id_comanda = carti_comandate.id_comanda
            group by clienti.id_client, nume, prenume
            having count(id_carte) > 5;
            ```	    

        * Returning the number of customers from each city (only cities that contain more than 2 customers)

            ```sql
            select count(id_client), oras
            from clienti
            group by oras
            having count(id_client) > 2
            order by count(id_client) asc;
            ```
  
        * Return of all ordered books

            ```sql      
            select * from carti c 
            join carti_comandate cc on c.id_carte = cc.id_comanda;
            ```

        * Return of ordered and delivered books

            ```sql
            select c.cod_carte, c.denumire_carte, l.mod_livrare
            from carti c 
            join carti_comandate cc on cc.id_carte = c.id_carte
            join livrare l on l.id_comanda = cc.id_comanda;
            ```
       
        * The return of all the books that were ordered as well as those that were not ordered

            ```sql
            select * from carti c 
            left join carti_comandate cc on c.id_carte = cc.id_carte;

            select * from carti_comandate cc
            right join carti c on cc.id_carte = c.id_carte;

            select * from comenzi c 
            right join livrare l on l.id_comanda = c.id_comanda;

            select * from carti c 
            cross join carti_comandate cc on c.id_carte = cc.id_carte;
            ```
 
        * The return of the number of books ordered for each author

            ```sql
            select c.autor, count(*)
            from carti_comandate cc
            inner join carti c on cc.id_carte = c.id_carte
            group by c.autor;
            ```

        * Return of all orders paid by cash

            ```sql
            select * from comenzi
            where tip_plata = (select id_modalitate_plata
						 from plata
						 where modalitate_plata = 'cash');
            ```
 
        * Return of all orders paid by Cash and Card

            ```sql
            select * from comenzi
            where tip_plata in (select id_modalitate_plata
					          from plata
					          where modalitate_plata in ('cash','card'));
            ```
          
      
  4. Conclusions

     I created a database for sell book online, from where I learned to create tables, populate them with data, make connections between tables, update some information, delete some data, and return the data both at once and with various filters.





