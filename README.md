# Week-3-SQL-Exercise
MariaDB [foy]> create table vets (lname varchar(100), fname varchar(100), town varchar(100), state varchar(20));
Query OK, 0 rows affected (0.008 sec)

# 1
MariaDB [foy]>  LOAD DATA LOCAL INFILE 'C:\\Users\\foyje\\Downloads\\VV.csv'INTO TABLE vets FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY'\n';
Query OK, 58253 rows affected (0.164 sec)
Records: 58253  Deleted: 0  Skipped: 0  Warnings: 0

MariaDB [foy]> select count(*) as RowCount from vets;
+----------+
| RowCount |
+----------+
|    58253 |
+----------+
1 row in set (0.010 sec)

# 2
MariaDB [foy]> SELECT count(*) FROM vets where trim(state) = state;
+----------+
| count(*) |
+----------+
|       83 |
+----------+
1 row in set (0.014 sec)

# 3
MariaDB [foy]> DELETE FROM vets WHERE lname = '' AND fname = '' AND town = '' AND state = '';
Query OK, 83 rows affected (0.029 sec)

# 4
MariaDB [foy]> UPDATE vets SET state = TRIM(state);
Query OK, 58170 rows affected (0.225 sec)
Rows matched: 58170  Changed: 58170  Warnings: 0

# 5
MariaDB [foy]> UPDATE vets SET lname = TRIM(lname);
Query OK, 8 rows affected (0.038 sec)
Rows matched: 58170  Changed: 8  Warnings: 0

MariaDB [foy]> UPDATE vets SET fname = TRIM(fname);
Query OK, 58170 rows affected (0.230 sec)
Rows matched: 58170  Changed: 58170  Warnings: 0

MariaDB [foy]> UPDATE vets SET town = TRIM(town);
Query OK, 58170 rows affected (0.223 sec)
Rows matched: 58170  Changed: 58170  Warnings: 0

MariaDB [foy]> SELECT fname as "First Name", lname as "Last Name", town, state from vets where fname like 'GUADALUPE%';
+-------------------+-----------+-------------+-------+
| First Name        | Last Name | town        | state |
+-------------------+-----------+-------------+-------+
| GUADALUPE MASIAS  | ALVAREZ   | DONNA       | TX    |
| GUADALUPE         | FLORES    | BEXAR       | TX    |
| GUADALUPE JR      | GALINDO   | ROCKPORT    | TX    |
| GUADALUPE B L     | GARIBAY   | SAN DIEGO   | CA    |
| GUADALUPE         | GONZALEZ  | ALICE       | TX    |
| GUADALUPE MENDOZA | LEAL      | QUITAQUE    | TX    |
| GUADALUPE         | LERMA     | EDCOUCH     | TX    |
| GUADALUPE         | MARTINEZ  | LAREDO      | TX    |
| GUADALUPE ESPARZA | MONTOYA   | ARGO        | IL    |
| GUADALUPE         | PEREZ     | SAN JOAQUIN | CA    |
| GUADALUPE JR      | PRADO     | MERCEDES    | TX    |
| GUADALUPE         | RENDON    | CASA GRANDE | AZ    |
| GUADALUPE NATAL   | ZUNIGA    | SAN ANTONIO | TX    |
+-------------------+-----------+-------------+-------+
13 rows in set (0.015 sec)

# 6
MariaDB [foy]> SELECT COUNT(*) from vets where town like 'Los%';
+----------+
| COUNT(*) |
+----------+
|      586 |
+----------+
1 row in set (0.028 sec)

# 7
MariaDB [foy]> SELECT COUNT(*) from vets where town like 'LOS ANGELES%';
+----------+
| COUNT(*) |
+----------+
|      538 |
+----------+
1 row in set (0.013 sec)

MariaDB [foy]> SELECT COUNT(*) FROM vets WHERE town LIKE 'LOS%' AND town <> 'LOS ANGELES';
+----------+
| COUNT(*) |
+----------+
|       48 |
+----------+
1 row in set (0.014 sec)

# 8
MariaDB [foy]> SELECT town, COUNT(*) FROM vets WHERE town LIke 'LOS%' GROUP BY town ORDER BY COUNT(*) DESC;
+-----------------+----------+
| town            | COUNT(*) |
+-----------------+----------+
| LOS ANGELES     |      538 |
| LOS ALTOS       |       10 |
| LOS GATOS       |        8 |
| LOS ALAMITOS    |        6 |
| LOS BANOS       |        4 |
| LOS ALAMOS      |        3 |
| LOST NATION     |        2 |
| LOS LUNAS       |        2 |
| LOS FRESNOS     |        2 |
| LOS MOLINOS     |        2 |
| LOST CREEK      |        2 |
| LOS PALOS       |        1 |
| LOS ALTOS HILLS |        1 |
| LOS CORDOVAS    |        1 |
| LOST HILLS      |        1 |
| LOS EBANOS      |        1 |
| LOS OLIVOS      |        1 |
| LOS NIETOS      |        1 |
+-----------------+----------+
18 rows in set (0.024 sec)

MariaDB [foy]> SELECT town, COUNT(*) FROM vets WHERE town Like 'LOS%' AND town <> 'LOS ANGELES' GROUP BY town ORDER BY COUNT(*) DESC;
+-----------------+----------+
| town            | COUNT(*) |
+-----------------+----------+
| LOS ALTOS       |       10 |
| LOS GATOS       |        8 |
| LOS ALAMITOS    |        6 |
| LOS BANOS       |        4 |
| LOS ALAMOS      |        3 |
| LOST CREEK      |        2 |
| LOST NATION     |        2 |
| LOS LUNAS       |        2 |
| LOS FRESNOS     |        2 |
| LOS MOLINOS     |        2 |
| LOS OLIVOS      |        1 |
| LOS NIETOS      |        1 |
| LOS PALOS       |        1 |
| LOS ALTOS HILLS |        1 |
| LOS CORDOVAS    |        1 |
| LOST HILLS      |        1 |
| LOS EBANOS      |        1 |
+-----------------+----------+
17 rows in set (0.013 sec)

# 9 
MariaDB [foy]> SELECT fname, lname, town, state FROM vets WHERE state = 'Gu' ORDER BY lname;
+---------------------+-------------+---------------------------+-------+
| fname               | lname       | town                      | state |
+---------------------+-------------+---------------------------+-------+
| JOSE QUINATA        | AGUON       | UMATAC                    | GU    |
| FRANCISCO M         | ASANOMA     | INARAJAN                  | GU    |
| DAVID GUERRERO      | BENAVENTE   | DEDEDO                    | GU    |
| MARK FREDERICK      | BIAGINI     | MANGILAO                  | GU    |
| ANTHONY MARTIN M    | BLAS        | YONA                      | GU    |
| JAMES LUJAN         | BLAZ        | DEDEDO                    | GU    |
| JUAN SANTOS         | BORJA       | AGANA                     | GU    |
| JOAQUIN PALACIOS    | CABRERA     | PIQUA MERIZO              | GU    |
| DAVID BITANGA       | CAMACHO     | TAMUNING                  | GU    |
| DONALD SUMINGUIT    | CARTER      | DEDEDO                    | GU    |
| JUAN PASCUAL R      | CASTRO      | MONGMONG                  | GU    |
| JUAN DUENAS         | CEPEDA      | DEDEDO                    | GU    |
| EDWARD CRUZ         | CRUZ        | INARAJAN                  | GU    |
| ENRIQUE SALAS       | CRUZ        | SANTA RITA                | GU    |
| JOSEPH AGUIGUI      | CRUZ        | MERICO                    | GU    |
| JOSEPH WILLIAM      | CRUZ        | AGANA HEIGHTS             | GU    |
| PEDRO AFLAGUE       | CRUZ        | AGANA                     | GU    |
| RONALD PEREZ        | CUASITO     | TAMVNING                  | GU    |
| ALLAN JAMES         | DAMIAN      | AGANA                     | GU    |
| HERMAN BORJA        | DE LEON     | AGANA                     | GU    |
| FREDERICO V         | DELA-CRUZ   | AGANA                     | GU    |
| EDWARD REYES        | DIAZ        | PITI                      | GU    |
| ALBERT BARCINAS     | DOYLE       | MERIZO                    | GU    |
| JOSE BAMBA          | DUENAS      | TOTO                      | GU    |
| RUDY EDEJER         | EAY         | TAMUNING                  | GU    |
| JUANITO MAIQUEZ     | ESCANO      | AGANA                     | GU    |
| VICENTE T           | ESPINOSA    | MERIZO                    | GU    |
| FERNANDO BARCINAS   | ESTEVES     | MERIZO                    | GU    |
| JOSEPH MARTIN       | EUSTAQUIO   | YONA                      | GU    |
| HAROLD JAMES JR     | FINNEY      | ASAN                      | GU    |
| BENNY SAN NICOLAS   | FLORES      | MERIZO                    | GU    |
| DAVID CRUZ          | FLORES      | AGANA                     | GU    |
| DAVID JOHN          | FUNES       | BARRIGADA                 | GU    |
| DAVID ATOIGUE       | GORTON      | TALOFOFO                  | GU    |
| PEDRO ROSARIO       | GUERRERO    | BARRIGADA                 | GU    |
| VINCENT FEJA        | GUERRERO    | SINAJANA                  | GU    |
| JOSE BABAUTA        | HERRERA     | AGAT                      | GU    |
| JESUS ROSA          | MARIANO     | MANGILAO                  | GU    |
| ROBERT L G          | MENDIOLA    | AGANA                     | GU    |
| JESUS QUINENE       | MENO        | INARAJAN                  | GU    |
| TOMAS REYES         | MESA        | AGAT                      | GU    |
| VINCENT PINAULA     | MOREHAM     | SINAJANA                  | GU    |
| EMILIO NINAISEN     | NEDEDOG     | AGAT                      | GU    |
| GREGORIO L          | PANGELINAN  | MONGMONG                  | GU    |
| PEDRO CABRERA       | PANGELINAN  | AGANA                     | GU    |
| HENRY PANGELINAN    | PEREDA      | AGANA                     | GU    |
| JOHN ANTHONY        | PEREZ       | DEDEDO                    | GU    |
| VICENTE DUENAS      | PEREZ       | MONGMONG                  | GU    |
| JOHNNY CRUZ         | QUENGA      | AGAT                      | GU    |
| JESUS AQUININGO     | QUIDACHAY   | UMATAC                    | GU    |
| TOMAS GARCIA        | REYES       | AGANA                     | GU    |
| EUGENE RAYMOND      | RIPPEL      | DEDEDO                    | GU    |
| THOMAS SALAS        | RIVERA      | AGAT                      | GU    |
| LUCAS HERRERA       | RODRIGUEZ   | AGAT                      | GU    |
| ANTONIO QUICHOCHO   | SABLAN      | YIGO                      | GU    |
| IGNACIO ESPINOSA    | SABLAN      | SANTA RITA                | GU    |
| JOHN TENERIO        | SABLAN      | AGANA                     | GU    |
| THOMAS QUICHOCHO    | SABLAN      | YIGO                      | GU    |
| RUFO SANTOS         | SAN NICOLAS | SINAJANA                  | GU    |
| VICTOR P            | SAN NICOLAS | INARAJAN                  | GU    |
| GEORGE SANTIAGO     | SANCHEZ     | UMATAC                    | GU    |
| ENRIQUE ROSARIO     | SANTOS      | SINAJANA                  | GU    |
| ERNEST PABLO        | SANTOS      | TALOFOFO                  | GU    |
| JAMES EDWARD ANDER  | SANTOS      | DEDEDO                    | GU    |
| RAFAEL SALAS        | SANTOS      | AGANA                     | GU    |
| JOHNNY SALAS        | TAITAGUE    | TALOFOFO                  | GU    |
| FRANCIS SAN NICOLAS | TORRE       | MANGILAO                  | GU    |
| PRISHARDO JOSE T    | TORRES      | AGANA                     | GU    |
| JAMES EDWARD        | VIOLETT     | ------------------------- | GU    |
| RALPHAEL SGAMBELLUR | YOKOI       | MONGMONG                  | GU    |
+---------------------+-------------+---------------------------+-------+
70 rows in set (0.029 sec)

# 10
MariaDB [foy]> CREATE TABLE STATES (State varchar(30), Abbreviation varchar(10) primary key);
Query OK, 0 rows affected (0.009 sec)

MariaDB [foy]> LOAD DATA LOCAL INFILE 'C:\\Users\\foyje\\Downloads\\States.csv' INTO TABLE STATES FIELDS TERMINATED BY ',' ENCLOSED by '"' LINES TERMINATED BY '\n';
Query OK, 52 rows affected, 1 warning (0.021 sec)
Records: 52  Deleted: 0  Skipped: 0  Warnings: 1

MariaDB [foy]> DESCRIBE STATES;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| State        | varchar(30) | YES  |     | NULL    |       |
| Abbreviation | varchar(10) | NO   | PRI | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
2 rows in set (0.039 sec)

MariaDB [foy]> SELECT * FROM STATES;
+----------------------+--------------+
| State                | Abbreviation |
+----------------------+--------------+
| State                | Abbreviati   |
| Alaska               | AK           |
| Alabama              | AL           |
| Arkansas             | AR           |
| Arizona              | AZ           |
| California           | CA           |
| Colorado             | CO           |
| Connecticut          | CT           |
| District of Columbia | DC           |
| Delaware             | DE           |
| Florida              | FL           |
| Georgia              | GA           |
| Hawaii               | HI           |
| Iowa                 | IA           |
| Idaho                | ID           |
| Illinois             | IL           |
| Indiana              | IN           |
| Kansas               | KS           |
| Kentucky             | KY           |
| Louisiana            | LA           |
| Massachusetts        | MA           |
| Maryland             | MD           |
| Maine                | ME           |
| Michigan             | MI           |
| Minnesota            | MN           |
| Missouri             | MO           |
| Mississippi          | MS           |
| Montana              | MT           |
| North Carolina       | NC           |
| North Dakota         | ND           |
| Nebraska             | NE           |
| New Hampshire        | NH           |
| New Jersey           | NJ           |
| New Mexico           | NM           |
| Nevada               | NV           |
| New York             | NY           |
| Ohio                 | OH           |
| Oklahoma             | OK           |
| Oregon               | OR           |
| Pennsylvania         | PA           |
| Rhode Island         | RI           |
| South Carolina       | SC           |
| South Dakota         | SD           |
| Tennessee            | TN           |
| Texas                | TX           |
| Utah                 | UT           |
| Virginia             | VA           |
| Vermont              | VT           |
| Washington           | WA           |
| Wisconsin            | WI           |
| West Virginia        | WV           |
| Wyoming              | WY           |
+----------------------+--------------+
52 rows in set (0.004 sec)

MariaDB [foy]>
