CREATE TABLE BOOK(BOOK_ID INTEGER PRIMARY KEY , TITLE VARCHAR(20), PUBLISHER_NAME VARCHAR(20), foreign key (PUBLISHER_NAME) references PUBLISHER(NAME),PUB_YEAR VARCHAR(20));

CREATE TABLE BOOK_AUTHOR(BOOK_ID INTEGER, foreign key (BOOK_ID)references BOOK(BOOK_ID),AUTHOR_NAME varchar(50));

CREATE TABLE PUBLISHER(NAME VARCHAR(20) PRIMARY KEY, ADRESS VARCHAR(20),PHONE INTEGER);

CREATE TABLE COPIES(BOOK_ID INTEGER , foreign key (BOOK_ID) references BOOK(BOOK_ID), BRANCH_ID INTEGER , foreign key (BRANCH_ID) references LIBRARY_BRANCH(BRANCH_ID), NO_OF_COPIES INTEGER);

CREATE TABLE BOOK_LENDING(BOOK_ID INTEGER , foreign key (BOOK_ID) references BOOK(BOOK_ID), BRANCH_ID INTEGER , foreign key (BRANCH_ID) references LIBRARY_BRANCH(BRANCH_ID), CARD_NO INTEGER, DATE_OUT date, DUE_DATE date);

CREATE TABLE LIBRARY_BRANCH(BRANCH_ID INTEGER PRIMARY KEY, BRANCH_NAME VARCHAR(20), ADDRESS VARCHAR(20));

insert into BOOK values (874556, 'footboll rules','aslam_nadaf',1987);
insert into BOOK_AUTHOR values(874556,'jabir');
insert into PUBLISHER values ('aslam_nadaf','indi',855245);
insert into COPIES values (874556, 87426,2);
insert into BOOK_LENDING values ( 874556,87426,589,'2022-11-10','2022-11-24');
insert into LIBRARY_BRANCH values (87426,'cse','indi');

insert into BOOK values (1234, 'Tesla','musk',2011);
insert into BOOK_AUTHOR values(1234,'Elon_musk');
insert into PUBLISHER values ('musk','indi',855245);
insert into COPIES values (874556, 87426,5);
insert into BOOK_LENDING values ( 874556,87426,589,'2022-11-10','2022-11-24');
insert into LIBRARY_BRANCH values (872426,'autonumus','america');

insert into BOOK values (1717, 'microsoft','gates',2000);
insert into BOOK_AUTHOR values(1234,'Bill_gates');
insert into PUBLISHER values ('gates','usa',855245);
insert into COPIES values (88888, 87426,5);
insert into BOOK_LENDING values ( 1234,87426,589,'2022-11-10','2022-11-24');
insert into LIBRARY_BRANCH values (88888,'software','usa');


insert into BOOK values (1719, 'accident','kannur',2000);
insert into BOOK_AUTHOR values(1719,'samarth');
insert into PUBLISHER values ('kannur','ashram',855245);
insert into COPIES values (56743, 87363,5);
insert into BOOK_LENDING values ( 56743,87363,589,'2022-11-10','2022-11-24');
insert into LIBRARY_BRANCH values (43562,'ethical','ashram');

insert into BOOK values (87414, 'the captain','moin',2005);
insert into BOOK_AUTHOR values(87414,'munaf');
insert into PUBLISHER values ('moin','bangalore',855245);
insert into COPIES values (87414, 438962,9);
insert into BOOK_LENDING values ( 87414,438962,589,'2022-10-20','2022-11-21');
insert into LIBRARY_BRANCH values (438962,'data_scientist','bangalore');

select * from BOOK;
select * from BOOK_AUTHOR;
select * from PUBLISHER;
select * from COPIES;
select * from BOOK_LENDING;
select * from LIBRARY_BRANCH;

DELETE FROM PUBLISHER where NAME = 'aslam_nadaf';

SELECT LB.BRANCH_NAME,B.BOOK_ID, B.TITLE, B.PUBLISHER_NAME, BA.AUTHOR_NAME, C.NO_OF_COPIES
FROM BOOK B, BOOK_AUTHOR BA, COPIES C
WHERE B.BOOK_ID = BA.BOOK_ID AND B.BOOK_ID = C.BOOK_ID,LIBRARAY_BRANCH LB
group by LB.BRANCH_NAME;

select CARD_NO
from BOOK_LENDING
where DATE_OUT BETWEEN '2022-10-21' AND '2022-11-21'
GROUP BY CARD_NO
HAVING COUNT(*)>3;
 
DELETE FROM BOOK WHERE BOOK_ID = 1719 ;

create view V_PUBLICATION AS
SELECT PUB_YEAR
FROM BOOK; 

SELECT * FROM V_PUBLICATION;

CREATE VIEW V_BOOKS AS
SELECT B.BOOK_ID, B.TITLE, C.NO_OF_COPIES
FROM BOOK B, COPIES C
WHERE B.BOOK_ID = C.BOOK_ID;

SELECT * FROM V_BOOKS;
