This SQL starter kit of code snippets goes beyond the basic SELECT statement.  Select distinct, filtering, aggregate functions and joins



Select Distinct
select distinct
eventname as 'event name', 
eventdetails as 'event details', 
eventdate as 'event date'
from
event
where
countryid = 5
order by
eventdate asc
limit 10;


Select with IN
select
id, city, country
from 
address
where 
city in ('new york','amsterdam');


Select with OR
select
id, city, country
from 
address
where 
city = 'new york'
or city = 'amsterdam';


Select with Count
select 
count(city)
from 
address


Select with Concatenate
select
concat(name,' : ',city)
from 
address;
select 
upper(concat(name,' : ',city))
from 
address;


Select with Like
select
id, city, country
from 
address
where 
city like 'au%';


Select with Case
select
id, city, country
from 
address
case when population < 100000  then 'low'
when population < 200000 then 'medium'
when population < 300000 then 'high'
else 'very high'
end as population_level
from city;


Aggregate functions
select
continent, avg(population)
from
country
group by
continent;


Inner join
select
c.code,
c.name,
cl.language
from
country c
inner join
countrylanguage  cl /*Results where the rows exist in both tables*/
on c.code = cl.countrycode
where 
c.continent='africa';


Left join
select
c.code,
c.name,
cl.language
from
country c
left join
countrylanguage cl /*Everything from table A and the rows that match in table B*/
on c.code = cl.countrycode
where 
cl.continent='africa';
