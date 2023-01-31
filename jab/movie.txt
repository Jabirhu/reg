create  table ACTOR(Act_Id int primary key, Name varchar(30), Act_Grades int);
create  table Director(Dir_Id int primary key, Dir_Name varchar(30), Dir_Phone int);
create  table Movies(Mov_Id int PRIMARY KEY, Mov_Title varchar(30), Mov_Year int, Mov_lang varchar(30),Dir_Id int , foreign key(Dir_Id) references Director(Dir_ID) on delete cascade);
create  table Movie_Caste(Act_Id int, foreign key(Act_Id) REFERENCES ACTOR(Act_Id) ON DELETE cascade, Mov_Id int, FOREIGN KEY(Mov_Id) references Movies(Mov_Id) on delete cascade, Role varchar(30));
create  table Rating(Mov_Id int, foreign key(Mov_Id) references Movies(Mov_Id) on delete cascade ,Rev_Stars int);

insert into ACTOR values(101, 'Jackson', 5);
insert into ACTOR values(103, 'Shushanth', 9);
insert into ACTOR values(111, 'Ranveeer', 8);
insert into ACTOR values(105, 'Abhishek', 4);
insert into ACTOR values(126, 'Varun Dhawan', 6);

insert into Director values (501, 'Anthony', 856422);
insert into Director values (503,'Hitchcock',985544 );
insert into Director values (504,'Arjun Reddy',985544 );
insert into Director values (506,'Manjunath',985544 );
insert into Director values (511,'Praveen',985544 );

insert into Movies values(302, 'The destination', 2022, 'Japanese', 501);
insert into Movies values(306, 'The ironman', 1996,'Chinese',501);
insert into Movies values(305, 'The Captain', 1986,'English',501);
insert into Movies values(389, 'Time', 2018,'French',503);
insert into Movies values(315,'Dear Comerades',2016,'Telugu', 511);


insert into Movie_Caste values (101, 302, 'Main Actor');
insert into Movie_Caste values (101, 306, 'Comedian');
insert into Movie_Caste values (101, 305, 'Villain');
insert into Movie_Caste values (111, 389, 'Co-Actor');
insert into Movie_Caste values (103, 315, 'Hero');

insert into  Rating values(302,4);
insert into  Rating values(306,3);
insert into  Rating values(305,8);
insert into  Rating values(389,8);
insert into  Rating values(315,6);


delete from Movies where Mov_Id = 302;

drop table Movie_Caste;
select * from Movie_Caste; 

select Mov_Title 
from   Movies M, Director D
where  M.Dir_Id = D.Dir_Id and Dir_Name = 'Hitchcock';
Rev_Stars
select    Mov_Title
from      Movies M, Movie_Caste MC
where     MC.Mov_Id = M.Mov_Id and MC.Act_Id in ( select Act_Id
                                              from   Movie_Caste MC
                                              group by Act_Id
                                              having count(Mov_Id)>2
                                              );
										
select Name, Mov_Year
from ACTOR A 
join Movie_Caste C   
on A.Act_Id = C.Act_Id join
Movies M
on M.Mov_Id = C.Mov_Id
where M.Mov_Year < 2000 and A.Name in (
select Name
from ACTOR A join Movie_Caste C   
on A.Act_Id = C.Act_Id join
Movies M
on M.Mov_Id = C.Mov_Id
where M.Mov_Year > 2015);  

select * from Movies;
select * from ACTOR;
select * from Movie_Caste;
select * from Rating ;
    

select Mov_Title ,Rev_Stars
from   Movies M, Rating R
where  M.Mov_Id = R.Mov_id and  Rev_Stars > 0
order by Mov_Title;

update Director set Dir_Name = 'Steven Spielberg' where Dir_Name = 'Praveen';

update Director D, Movies M, Rating R
set Rev_Stars = 5
where D.Dir_Id = M.Dir_Id and M.Mov_Id = R.Mov_Id and  Dir_Name = 'Steven Spielberg';
