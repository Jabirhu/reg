create table Salesman(Salesman_Id int primary key, Name varchar(20), city varchar(20), commission varchar(20));

create table Customer(Customer_id int primary key, Cust_Name varchar(20), City varchar(20), Grade varchar(20), Salesman_id int , foreign key(Salesman_id) references Salesman(Salesman_Id) );

create table Orders(Ord_No int primary key, Purchase_Amt int, Ord_Date date, Customer_id int, foreign key(Customer_id) references Customer(Customer_id),Salesman_id int , foreign key(Salesman_id) references Salesman(Salesman_id) );

insert into Salesman values(152, 'Nasir', 'Bengaluru', 'Director');
insert into Salesman values(1000, 'Sampath', 'Shivamogga', 'Assisstant');
insert into Salesman values(154, 'Abhi', 'Kodur', 'Co-Dire');
insert into Salesman values(155, 'Abhishek', 'Belgaum', 'Designer');
insert into Salesman values(156, 'Likhith', 'Bhopal', 'Producer');


insert into Customer values(101, 'John', 'Bengaluru', 5,152);
insert into Customer values(102, 'Vinayak', 'Belgaum', 8,155);
insert into Customer values(103, 'Michael', 'Bengaluru', 3,152);
insert into Customer values(104, 'Shrikant', 'Belgaum', 7,155);
insert into Customer values(105, 'Abraham', 'Shivamogga', 4,1000);


insert into Orders values(201, 20000, '2012-10-10', 101, 152);
insert into Orders values(202, 40000, '2022-11-10', 102, 155);
insert into Orders values(203, 25000, '2022-10-18', 103, 152);
insert into Orders values(204, 30000, '2018-09-30', 104, 155);
insert into Orders values(205, 80000, '2002-11-23', 105, 1000);


alter table Customer add Grade int;

update Orders
set Salesman_Id = 1000
where Salesman_Id = 153;

drop table Salesman;

select count(*)
from Customer
where Grade > (
				Select avg(Grade)
                from Customer
                where City = 'Bengaluru'

)
;

select * from Salesman;
select * from Customer;
select * from Orders;

select Name , count(*) as No_of_Customers
from Salesman S , Customer C
where S.Salesman_Id = C.Salesman_Id
group by Name
having count(*) >1;

Select Name
from Salesman S , Customer C
where S.Salesman_Id = C.Salesman_Id
group by Name

union
(
 select Name
 from Salesman
 where Salesman_Id not in (
                            select S.Salesman_Id
                            from Salesman S , Customer C   
                            where S.Salesman_Id = C.Salesman_Id
 
 )

 );
 
create view  Highest_Salesman1 as
select Name, Purchase_Amt
from  Salesman S, Orders O
where S.Salesman_Id = O.Salesman_Id and Purchase_Amt in (
 
select max(Purchase_Amt)
from  Salesman S, Orders O
where S.Salesman_Id = O.Salesman_Id
);


select * from Highest_Salesman1;

delete  from Customer
where Customer_id = 101;
set foreign_key_checks=0;