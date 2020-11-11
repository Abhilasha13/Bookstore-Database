# Bookstore_Database
Implemented conceptual, logical, and physical data model designs using advanced SQL, ERD.

## Introduction
Bookman’s Entertainment Exchange is a used bookstore chain with 6 locations across Arizona. Besides books, they also sell computer/console games and dvds. The stores are staffed by clerks who work in shifts and each shift has a reporting manager.

## Detailed Requirements Analysis
Bookman’s has 6 locations throughout Arizona. Each store location has a store email account, phone number, and adress including the street, city, state, and zipcode. The stores are also assigned a name and unique store ID number.

Bookman’s customers can both buy and sell goods to the company. For both types of transactions, the purchase orders and sale orders are tracked. For the customers, Bookman’s keeps track of the customer ID, their first and last name, phone number, email, date of birth, gender, address, and the number of store credits assigned to their customer account when they sell goods to Bookman’s.

For goods that Bookman’s purchases, a purchase order ID generated, and they track the total amount paid to the customer, the purchase date, and the quantity of item copies purchased. Each individual item copy purchased is logged into a purchase units ledger, along with the acquisition price for the item. Bookman’s may purchase item copies from a single customer many times, but each particular purchase order is tied to a single customer. For each item copy purchased, there is only one purchase order associated with that item copy.

Once acquired, individual item copies are logged into inventory items, and Bookman’s assigns an item_copyID and tracks the condition, time the item was logged into inventory, the current status of the item copy, and the type (book, game, or DVD). Asking price is calculated based on the original list price of the item, the rating, and the condition of the copy. For each item copy purchased, there is one entry in the inventory.

When copies of items are logged into inventory, they are assigned to a specific store location.  Depending on the number of copies at the acquiring location, the new item copy may be assigned to another store location. The details of these inventory shipments include the acquiring storeID, the destination storeID, the date the item copy was logged into inventory, and the arrival date at the destination store. For each item copy, it is assigned to one store.

When item copies are sold, Bookman’s tracks the sales orders by assigning each a unique ID, as well as recording the sale date, quantity of item copies sold, and the total monetary value of the sale. The details are captured in a separate table that includes the price for each individual copy. This is linked to the customer account as well. Each item copy sold is tied to one particular sales order, but sales orders may have many item copies. Bookman’s may sell to the customer many times, but each sale order is tied to a particular customer account.

Bookman’s also maintains a database of the types of books, games, and dvds that customer could potentially bring into the store. For this, they assign a unique itemID, record the title, universal product code (UPC), the original list price for the item, the average review rating based on Amazon’s average customer rating for the item, type (whether it is a book, game, or dvd), and the release or publication date for the item.

Additional details are tracked for each type of item that could potentially be acquired by Bookman’s. For books, Bookman’s tracks the first, middle, and last name of the author and there could be more than one author for each title. They also track the number of pages, edition, binding, genre, and publisher name for each book. For the games, Bookman’s tracks the platform that the game runs on, the game publisher, the game developer, the age rating, and version of the game. For the dvds, they track the actor first and last names and there may be more than one actor associated with each dvd title. They also track the director’s first and last names and the producers first and last names. Even if there is more than one director or producer involved, they only track the top billed one. They also track the age rating, version, and runtime for each dvd title.

Store also host in-store events. They have several type of events which they host, and each event can be repeated on a different date and time. For the events, they assign a unique eventID and also have a unique number assigned to each event instance. For the event types, they track the event name, description, budget, and whether it is a kid’s event or not. Each store can host many types of events and many event instances. However, a particular event instance is located at a particular store. The same event can be held at multiple stores.

Bookman’s also collects applications from applicants in response to job openings. For the applicants, they assign a unique tracking number, and they collect the first and last names of applicants, the gender, date of birth, the resume, personal email, and address including the street, city, state, and zipcode. They also track specific skills that candidates have, and there may be more than one skill per applicant. Lastly, they track whether the applicant has a disability, and if so, a description of the disability.

Applicants respond to job openings. Postings are tied to a specific store, but there can be more than opening at each store. The postings include a requisition ID, job title, description of the job, the posting date and closing date for the open position, and compensation information for the role. Job title and descriptions can vary slightly between each position, and so are considered unique. When applicants apply to a specific job opening, Bookman’s records the date the application was both submitted and reviewed, as well as the status of the application. Each applicant apply to many job openings and there may be many applicants for the same opening. Each employee was once an applicant, but an applicant may or may not become an employee.

Bookman’s also keeps track of their employees. They assign a unique employee ID number to each employee, and record the first and last name of the employee, a description of the specific job the employee is assigned to, the employee type, base salary, bonus amount, and store emailID. Employees are also broken out into the specific employee types. For the managers, they track the department name. For the clerks, they also track the department name. For the technicians, they track the rank of the technician as well as the quality of instruments that technician is able to service. Employees may supervise other employees. While managers are supervisors, technicians can also be supervisors so Bookman’s is requesting the flexibility of assigning multiple employee types as supervisors. Each employee has one supervisor, but supervisors may manage multiple employees.

Managers and clerks are grouped into shifts for scheduling purposes (technicians work a straight schedule and their schedule does not need to be incorporated into the database). Each shift has a unique shiftID, a specific start and end time, and day of the week. Every shift has one and only one manager assigned and there must be at least 4 clerks in each shift. Shifts are ties to a particular store but each store is staffed using multiple shifts.

Each store has one service center within it. Within the service center, Bookman’s assigns a service centerID and tracks the name of the service center, the phone number for the service desk, email account for the service center, and the opening hours, closing hours, and day of the week in which the service center is closed.
Each service center offers several different types of instrument repair. For each service type offered, they track a unique sericeID number, the cost of the service, the average time it takes to do the service, a description, severity level, and whether or not the service is covered by a warranty. When services are rendered, the customer is issued an invoice. Each invoice has a separated ID, and Bookman’s tracks the bill date and bill amount. Each service has one bill associated with it, although customers may have more than one service instance and associated invoice.

These services can be grouped into categories based on problem types. Each problem type has a unique identifier problem_typeID, a problem description, severity level, root cause, and recommended solution. Technicians are assigned to work on a particular instrument repair ticket (also called an escalation). Each technician is trained on several type of problems and can handle repairs associated with those types. For each ticket, Bookman’s records the escalation date, description, type of ticket, and a unique ID. Each ticket is associated with only one service instance, but one service instance may have multiple tickets associated with it.

## CONCEPTUAL SCHEMA
The conceptual schema for the database is shown in Fig.1. 

### Figure 1: Entity Relationship (ER) Diagram for Bookman's Entertainment Exchange
[Entity Relationship (ER) Diagram](https://github.com/Abhilasha13/Bookstore_Database/blob/main/ER_diagram.pdf)

## RELATIONAL SCHEMA
A list of the translated relations is below. 

```
APPLICANT_SKILLS(applicantID, skill_name)
APPLICANTS(applicantID, f_name, l_name, street, city, state, zipcode, gender, resume, disability, disability_description, DOB, email, phone)
APPLICATION_DETAILS(applicantID, job_openingID, date_submitted, date_reviewed, status)
BILLING_DETAILS(custID, serviceID, invoiceID, bill_amount, bill_date)
BOOK_AUTHORS(bookID, author_f_name, author_m_name, author_l_name)
CAN_HANDLE(problem_typeID, technicianID)
CUSTOMER_SERVICE_TICKET(custID, serviceID)
CUSTOMERS(custID, f_name, l_name, phone, email, street, city, state, zipcode, gender, DOB, customer_credits)
DVD_ACTORS(dvdID, actor_f_name, actor_l_name)
EMPLOYEES(empID, f_name, l_name, base_salary, bonus, employee_type, applicantID, reporting_managerID, emp_emailID)
CLERK(clerkID, department_name)
MANAGER(managerID, department_name)
TECHNICIAN(technicianID, technician_rank, instrument_quality)
ESCALATIONS(escalationID, serviceID, escalation_type, description, escalation_date, technicianID)
EVENT_HOST(eventID, storeID)
EVENT_INSTANCES(event_instanceID, event_date, event_time, eventID, storeID)
EVENTS(eventID, event_name, description, kid_friendly, budget)
GAME_PLATFORM(gameID, platform)
INVENTORY_DETAILS(item_copyID, acq_storeID, dest_storeID, login_date, arrival_date, status)
INVENTORY_ITEMS(item_copyID, condition, sale_price, status, type, itemID, time_created)
BCOPY(bcopy, bookID)
DCOPY(dcopyID, dvdID)
GCOPY(gcopyID, gameID)
ITEMS(itemID, title, list_price, UPC, release_date, item_type, review_rating)
BOOKS(bookID, ISBN, pubname, numpages, binding, genre, edition)
DVDS(dvdID, ISAN, director_f_name, director_l_name, producer_f_name, producer_l_name, runtime, version, agerating)
GAMES(gameID, GP1, agerating, publisher, developer)
JOB_OPENING(job_openingID, job_title, job_description, salary_type, posting_date, closing_date, storeID)
PROBLEM_TYPES(problem_typeID, problem_description, solution_recommended, problem_severance_rating, root_cause)
PURCHASE_ORDERS(purchse_orderID, purchase_amount, quantity, custID, purchase_date)
PURCHASE_UNITS(purchase_orderID, item_copyID, acquisition_price)
SALE_ORDERS(sale_orderID, sale_date, bill_amount, quantity, custID)
SALE_UNITS(sale_orderID, item_copyID, price)
SERVICE_CENTER(service_centerID, service_center_name, phone, email, opening_hour, closing_hour, day_closed)
SERVICE_HANDLING(serviceID, service_centerID)
SERVICES(serviceID, problem_typeID, technicianID, service_cost, avg_service_time, service_description, service_warranty, severance_level)
SHIFT_CREWS(shiftID, empID)
STORES(storeID, store_name, phone, email, street, city, state, zipcode, service_centerID)
```

## QUERIES
Structured query language is a standard database language that is used to create, maintain and retrieve the relational database.

Bookman’s being the largest used book-seller in Arizona, deals with numerous items and needs to keep a track of these items in its database and retrieve the required details whenever needed. In order to facilitate their Business requirements, we have developed a few queries which would help in their Business.

### QUERY 1:
Bookman’s deals with the purchase and sale of used items. For the purpose of our project we are tracking only three items i.e. Books, DVDs and Games. The below query gives the total count of the books, dvds and games purchased and sold by Bookman’s till now along with the top 3 items that were purchased and sold in each category.
Code:
```
With PSOLD as (SELECT distinct  ITEM_TYPE,coalesce(listagg(TITLE,',') within group (order by ranking),'N/A')
as Top_Tiltles  FROM 
(
  select distinct i.ITEMID,i.TITLE,i.ITEM_TYPE,COUNT(i.ITEMID),DENSE_RANK()OVER(ORDER BY COUNT(ii.ITEMID)DESC) as ranking
  from ITEMS i
  inner join inventory_items ii on ii.itemid = i.itemid
  inner join sale_units su on su.item_copyid = ii.item_copyid
  --WHERE item_type = 'GAME' 
  GROUP BY i.ITEMID,i.TITLE,i.ITEM_TYPE)
  WHERE RANKING <=3
  GROUP BY ITEM_TYPE
 ),

PPURC as (SELECT distinct  ITEM_TYPE,coalesce(listagg(TITLE,',') within group (order by ranking),'N/A')
  as Top_Tiltles  FROM 
  (
  select distinct i.ITEMID,i.TITLE,i.ITEM_TYPE,COUNT(i.ITEMID),DENSE_RANK()OVER(ORDER BY COUNT(ii.ITEMID)DESC) as ranking
  from ITEMS i
  inner join inventory_items ii on ii.itemid = i.itemid
  inner join purchase_units pu on pu.item_copyid = ii.item_copyid
  --WHERE item_type = 'GAME' 
  GROUP BY i.ITEMID,i.TITLE,i.ITEM_TYPE)
  WHERE RANKING <=3
  GROUP BY ITEM_TYPE
 )

SELECT 'Items Sold', i.item_type as "Type of Items", count(i.itemid) as "Total number of Items",
PSOLD.Top_Tiltles as "Top 3 Items"
from ITEMS i
inner join inventory_items ii on ii.itemid = i.itemid
inner join sale_units su on su.item_copyid = ii.item_copyid
inner join PSOLD on i.item_type = PSOLD.item_type
group by i.item_type,PSOLD.Top_Tiltles

UNION all

SELECT 'Items Purchased',i.item_type as "Type of Items", count(i.itemid) as "Total number of Items",
PPURC.Top_Tiltles as "Top 3 Items"
from ITEMS i
inner join inventory_items ii on ii.itemid = i.itemid
inner join purchase_units pu on pu.item_copyid = ii.item_copyid
inner join PPURC on i.item_type = PPURC.item_type
group by i.item_type,PPURC.Top_Tiltles;
```
![Total Count of Items Sold](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/total_count_of_items_sold.png)

### QUERY 2: 
One of the modules of Bookman’s is its Instruments Service Center. The Bookman’s deals with purchasing and selling the instruments and also maintains a service center to repair any instrument. Hence, it is really important for Bookman’s to maintain a record of total number of services provided or escalations raised in order to make sure things are on track and the Service Centers are functioning properly. The below query explains the different problem types that the Service Centers deal with, its description and severity along with the total number of escalations raised for each service, number of escalations raised within a month and the number of escalations which are raised within a month and are still unresolved.

This query can be used for audit purpose to make sure any escalation that is raised is taken care of as soon as possible.

Code:
```
WITH PESC as (select serviceid,count(escalationid) as num_escalation from escalations WHERE 
  ESCALATION_TYPE in ('not resolved', 'partially resolved') group by serviceid),
  PMON as (select PESC.serviceid as serviceid, PESC.num_escalation as num_escalation_mon from escalations e inner join PESC on PESC.serviceid = e.serviceid WHERE 
  (ESCALATION_DATE >= (SYSDATE - 30) AND ESCALATION_CLOSE_DATE <= sysdate)),

PRES as (select PMON.serviceid, PMON.num_escalation_mon as open_escalations from escalations e 
  inner join PMON on PMON.serviceid = e.serviceid 
  WHERE e.ESCALATION_CLOSE_DATE IS NULL)

select st.storeid as "Store Name", pt.PROBLEM_TYPEID, PROBLEM_DESCRIPTION, PROBLEM_SEVERENCE_RATING as "Severity Rating", count(s.serviceid) as Number_of_tickets_raised,
sum(PESC.num_escalation) as "Number of Escalations",PMON.num_escalation_mon as "Num Escalations within a month",
PRES.open_escalations as "Still Unresolved"
FROM problem_types pt inner join services s on s.PROBLEM_TYPEID = pt.PROBLEM_TYPEID
inner join escalations e on e.serviceid = s.serviceid
inner join PESC on s.serviceid = PESC.serviceid
inner join service_handling sh on sh.serviceid = s.serviceid
inner join stores st on st.service_centerid = sh.service_centerid
left outer join PESC on s.serviceid = PESC.serviceid
left outer join PMON on s.serviceid = PMON.serviceid
left outer join PRES on s.serviceid = PRES.serviceid
group by  pt.PROBLEM_TYPEID, PROBLEM_DESCRIPTION, PROBLEM_SEVERENCE_RATING,st.storeid,PMON.num_escalation_mon,PRES.open_escalations
order by st.storeid;
```
![Service Center Details](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/service_center_details.png)

### QUERY 3:
Bookman’s requires to maintain the total summary of the items that are being sold and purchased. They need to track and record the total purchase in the past years, past months too, in order to understand how they are performing in the market. The below query gives calculated the total number of items purchased by Bookman’s in the past 24 months, previous month, next month, etc. This helps the Board of Directors to obtain a comparative evaluation and to understand how the store is performing overall.

Code:
```
WITH time_per as (select add_months(sysdate,-24) as req_time from dual),
  listmonths (mon_only) AS (SELECT req_time as mon_only FROM time_per
  UNION ALL 
  SELECT add_months(mon_only,1) FROM listmonths WHERE add_months(mon_only,1) <= sysdate), 
  monyear as (SELECT extract(year from mon_only) as req_year, extract(month from mon_only) as mon_only FROM listmonths
 ),

PCHEK as (
  SELECT ii.item_copyID, ii.type, extract(year from p.purchase_date) as year1, extract(month from p.purchase_date) as month1
  FROM time_per, inventory_items ii
  JOIN purchase_units pu ON ii.item_copyid = pu.item_copyid
  JOIN purchase_orders p ON p.purchase_orderID = pu.purchase_orderID
  where p.purchase_date >= time_per.req_time
),

PTOTAL as (
  SELECT year1, month1, count(*) as Pyear_mon FROM PCHEK
  GROUP BY year1, month1), 
  PSALES as (SELECT req_year, mon_only, coalesce(Pyear_mon,0) checkouts_1 FROM monyear my 
  LEFT OUTER JOIN PTOTAL mb on my.req_year = mb.year1 and my.mon_only = mb.month1
), 

Ptot as (
  SELECT req_year, mon_only, checkouts_1,
  COALESCE(To_char(lag(checkouts_1,1) OVER (PARTITION BY mon_only ORDER BY req_year ,mon_only)),'N/A') as "Last Year's Checkouts",
  COALESCE(to_char(lead(checkouts_1,1) OVER (order by req_year desc,mon_only desc )),'N/A') as "Last Month's Checkouts",
  COALESCE(to_char(lag(checkouts_1,1) OVER (ORDER BY req_year DESC,mon_only desc)),'N/A') as "Next Month's Checkouts",
  COALESCE(To_char((checkouts_1 - lag(checkouts_1,1) OVER (PARTITION BY mon_only ORDER BY req_year ,mon_only))),'N/A') as "Annual Change",
  COALESCE(To_char((checkouts_1 - lead(checkouts_1,1) OVER (order by req_year desc,mon_only desc ))),'N/A') as "Monthly Change",
  coalesce(sum(checkouts_1) OVER (partition by req_year order by mon_only), 0) AS ytdc
  FROM PSALES
)

SELECT  to_char(to_date(mon_only,'MM'),'Month')||'- '||req_year as "Year and Month",  checkouts_1 AS "Checkouts",
"Last Year's Checkouts","Last Month's Checkouts" as "Last Month's Checkouts", "Next Month's Checkouts" as "Next Month's Checkouts",
"Annual Change" as "Annual change","Monthly Change" as "Monthly change",ytdc as "YTD Checkouts" FROM Ptot
ORDER BY req_year desc, mon_only desc
FETCH FIRST 24 rows only
```
![Past 24 months details](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/items_purchased_in_past_24_months.png)

### QUERY 4:
Apart from maintaining the purchase history, Bookman also needs to maintain  the sales history. The current and the above queries are similar, but they are required as per the Business logic by Bookman’s.

Code:
```
WITH time_per as (
  select add_months(sysdate,-24) as req_time from dual),
  listmonths (mon_only) AS (SELECT req_time as mon_only FROM time_per
  UNION ALL 
  SELECT add_months(mon_only,1) FROM listmonths WHERE add_months(mon_only,1) <= sysdate), 
  monyear as (SELECT extract(year from mon_only) as req_year, extract(month from mon_only) as mon_only FROM listmonths
),

PCHEK as (
  SELECT ii.item_copyID, ii.type, extract(year from s.sale_date) as year1, extract(month from s.sale_date) as month1
  FROM time_per, inventory_items ii
  JOIN sale_units su ON ii.item_copyid = su.item_copyid
  JOIN sale_orders s ON s.sale_orderID = su.sale_orderID
  where s.sale_date >= time_per.req_time
),

PTOTAL as (
  SELECT year1, month1, count(*) as Pyear_mon FROM PCHEK
  GROUP BY year1, month1), 
  PSALES as (SELECT req_year, mon_only, coalesce(Pyear_mon,0) checkouts_1 FROM monyear my 
  LEFT OUTER JOIN PTOTAL mb on my.req_year = mb.year1 and my.mon_only = mb.month1
),

Ptot as (
  SELECT req_year, mon_only, checkouts_1,
  COALESCE(To_char(lag(checkouts_1,1) OVER (PARTITION BY mon_only ORDER BY req_year ,mon_only)),'N/A') as "Last Year's Checkouts",
  COALESCE(to_char(lead(checkouts_1,1) OVER (order by req_year desc,mon_only desc )),'N/A') as "Last Month's Checkouts",
  COALESCE(to_char(lag(checkouts_1,1) OVER (ORDER BY req_year DESC,mon_only desc)),'N/A') as "Next Month's Checkouts",
  COALESCE(To_char((checkouts_1 - lag(checkouts_1,1) OVER (PARTITION BY mon_only ORDER BY req_year ,mon_only))),'N/A') as "Annual Change",
  COALESCE(To_char((checkouts_1 - lead(checkouts_1,1) OVER (order by req_year desc,mon_only desc ))),'N/A') as "Monthly Change",
  coalesce(sum(checkouts_1) OVER (partition by req_year order by mon_only), 0) AS ytdc
  FROM PSALES
)

SELECT  to_char(to_date(mon_only,'MM'),'Month')||'- '||req_year as "Year and Month",  checkouts_1 AS "Checkouts",
"Last Year's Checkouts","Last Month's Checkouts" as "Last Month's Checkouts", "Next Month's Checkouts" as "Next Month's Checkouts",
"Annual Change" as "Annual change","Monthly Change" as "Monthly change",ytdc as "YTD Checkouts" FROM Ptot
ORDER BY req_year desc, mon_only desc
FETCH FIRST 24 rows only
```
![Sales History](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/sales_history.png)

### QUERY 5:
Bookman Store also conducts events. These events can be conducted at different locations also. Bookman’s needs to keep a track of the events conducted by them along with the budget and many other details. This query gives the details of total number of events conducted, total budget spent on each events and the total number of kid-friendly events.

Code:
```
With a as (
  Select s.storeid as sid, s.store_name as sname, e.Eventid, e.event_name,e.budget
  from events e join event_instances ei on e.eventid = ei.eventid
  join stores s on s.storeid = ei.storeid 
  order by s.store_name
),

b as ( 
  Select s.storeid as sid, count(e.Eventid) as count_of_event, sum(e.budget) as kid_budget
  from events e join event_instances ei on e.eventid = ei.eventid
  join stores s on s.storeid = ei.storeid
  where kid_friendly = 'Y'
  group by s.storeid
  order by sid
),

c as( 
  Select a.sid, a.sname, nvl(count(a.eventid),0) as tec, 
  nvl(b.count_of_event,0) as tkfe,
  sum(a.budget) as totalSpend,
  nvl(b.kid_budget,0) as tske
  from a full outer join b on a.sid = b.sid
  group by a.sid, a.sname, nvl(b.count_of_event,0), nvl(b.kid_budget,0)
  order by sid
),
d as(
  Select c. sid, c.sname, c.tec, 
  c.tkfe, c.totalSpend, 
  c.tske, (c.totalSpend - c.tske) as abc,
  Round((c.tske*100/c.totalSpend),2)
  from c
)

Select d. sid as "Store ID", d.sname as "Store Name", d.tec as "Total Events Conducted", 
d.tkfe as "Total Kids events conducted", d.totalSpend as "Total Spending on All events", 
d.tske as "Total Spending on Kids events", 
(d.totalSpend - d.tske) as "Total Spending on other events",
(Round((d.tske*100/d.totalSpend),2))||'%' as "Percent spend on kids events", 
Round((d.abc*100/d.totalSpend),2)||'%' as "Percent spend on other events"
from d;
```

![Event Details](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/event_details.png)

### QUERY 6:
As a part of the Business, Bookman’s also needs to track the Customer details, in order to keep a track of their faithful customers. This Query helps Bookmans to generate a list of customers and rank them according to the sale amount and purchase amount. Customers are being ranked on the basis of the purchase amount and the sale amount. 
The Ranks are separate for purchase and sales. Using the data generated by this query  Bookmans can provide future points and discounts to its top ranked customers.

Code:
```
With a as (
  Select c.custid, c.f_name ||' '|| c.l_name as Customer_Name, SUM(purchase_amount) as TotalAmount, SUM(po.quantity) as qp,
  SUM(so.bill_amount) as bill_amount,
  SUM(so.quantity) as qs
  from purchase_orders po join
  customers c on po.custid = c.custid
  join sale_orders so on so.custid = c.custid
  where purchase_amount is not null
  group by c.custid, c.f_name, c.l_name
  order by TotalAmount Desc
),

b as (
  Select a.custid,a.TotalAmount,
  DENSE_RANK() over (order by a.TotalAmount desc) my_rank
  from a
),

c as (
  Select a.custid, a.bill_amount,
  DENSE_RANK() over (order by a.bill_amount desc)my_rank
  from a
)

Select a.custid as "Customer ID",
a.Customer_Name as "Customer Name",
a.qp as "Purchase items Quantity", 
b.totalamount as "Total Purchase Amount", 
b.my_rank  as "Customer Rank - Purchase",
a.qs as "Sold items Quantity", 
a.bill_amount as "Total Sale Amount",
c.my_rank as "Customer Rank - Purchase"
from a join b on a.custid = b.custid
join c on a.custid = c.custid;
```
![Customer Ranking](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/customer_ranking.png)

### Query 7:
Apart from maintaining the total report, budget and customer details, Bookman’s also tracks the details of book/game/dvd copies in stock and in which store and their category (must buy, good buy, average buy) and the date since they first became available in the store. This helps them in understanding which items are useful for the store, which itemcan be purchased from their customers and which items are in demand.

Code:
```
select i.TITLE as "Title", i.item_type as "Category",s.store_name as "Available in Stores",i.review_rating as "User Rating",
(select trunc(min(time_created)) from inventory_items where inventory_items.itemid = i.itemid) as "Available Since",
case 
  when i.review_rating > 4.5 then 'Must Buy'
  when i.review_rating > 4.0 then 'Good Buy'
  when i.review_rating > 3.5 then 'Average Buy'
  else 'ok to buy'
 end as "User Values",
 count(*) as "Total Copies Available"
 from INVENTORY_ITEMS ii
 JOIN items i ON ii.itemid = i.itemid
 join inventory_details id ON id.item_copyid = ii.item_copyid
 join stores s on s.storeid = id.dest_storeid
 where id.STATUS = 'In Stock' 
 group by i.TITLE,i.item_type, s.store_name,id.dest_storeid,i.review_rating,i.itemid
```
![Item Details](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/item_details.png)

### Query 8:
Since Bookman’s major focus is the inventory modules, we have tried to get all the details that it will require for its Business.  This query calculates the total purchase of books, dvd and games at a store along with total sales of books, DVD and games at the store. This also illustrates the total profit at a store till date.

Code:
```
with sale_det as
  (select * from 
  (select strid, strname,itmtype,saleprice
  from (select id.DEST_STOREID strid,s.store_name strname,su.ITEM_COPYID,i.ITEM_TYPE itmtype,su.PRICE saleprice
  from SALE_UNITS su
  join INVENTORY_ITEMS ii ON su.item_copyid = ii.item_copyid
  JOIN ITEMS i ON ii.ITEMID = i.ITEMID
  join inventory_details id ON id.ITEM_COPYID = su.ITEM_COPYID
  join STORES s ON s.STOREID = id.DEST_STOREID)
  )
  pivot
  (
  SUM(saleprice)
      for itmtype in ('GAME' "GAME_SALES",'dvd' "DVD_SALES",'BOOK' "BOOK_SALES") 
  )
),
acqisition_det as 
(
  select * from 
  (select strids, strnames,itmtypes,acqprice
  from (select id.ACQ_STOREID strids,s.store_name strnames,pu.ITEM_COPYID,i.ITEM_TYPE itmtypes,pu.ACQUISITION_PRICE acqprice
  from PURCHASE_UNITS pu
  join INVENTORY_ITEMS ii ON pu.item_copyid = ii.item_copyid
  JOIN ITEMS i ON ii.ITEMID = i.ITEMID
  join inventory_details id ON id.ITEM_COPYID = pu.ITEM_COPYID
  join STORES s ON s.STOREID = id.ACQ_STOREID)
  )
  pivot
  (
  SUM(acqprice)
      for itmtypes in ('GAME' "GAME_PURCHASE",'dvd' "DVD_PURCHASE",'BOOK' "BOOK_PURCHASE") 
  )
)

SELECT sale_det.strid as "STORE ID",
sale_det.strname as "Store Name",  
to_char(coalesce(sale_det."BOOK_SALES",0),'$999999.99') as "Total Book Sales", 
to_char(coalesce(sale_det."DVD_SALES",0),'$999999.99') as "Total DVD Sales",
to_char(coalesce(sale_det."GAME_SALES",0),'$999999.99') as "Total Game Sales",
to_char(coalesce(sale_det."BOOK_SALES",0)+coalesce(sale_det."DVD_SALES",0)+coalesce(sale_det."GAME_SALES",0),'$999999.99') as "Total Sales",
to_char(coalesce(acqisition_det."BOOK_PURCHASE",0),'$999999.99') as "Total Book PURCHASE", 
to_char(coalesce(acqisition_det."DVD_PURCHASE",0),'$999999.99') as "Total DVD PURCHASE",
to_char(coalesce(acqisition_det."GAME_PURCHASE",0),'$999999.99') as "Total Game PURCHASE",
to_char(coalesce(acqisition_det."BOOK_PURCHASE",0)+coalesce(acqisition_det."DVD_PURCHASE",0)+coalesce(acqisition_det."GAME_PURCHASE",0),'$999999.99') as "Total PURCHASE",
to_char((coalesce(sale_det."BOOK_SALES",0)+coalesce(sale_det."DVD_SALES",0)+coalesce(sale_det."GAME_SALES",0)) -(coalesce(acqisition_det."BOOK_PURCHASE",0)+coalesce(acqisition_det."DVD_PURCHASE",0)+coalesce(acqisition_det."GAME_PURCHASE",0)),'$999999.99') as "Total Profit per store"
FROM sale_det
JOIN acqisition_det
ON sale_det.strid = acqisition_det.strids
order by strids;
```
![Profit Details](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/profit_details.png)

### Query 9:
In the below query, we try to calculate the total number of items available in the inventory in different months of a year. This would be helpful to generate details of each month in a financial year and later it can also be helpful to track the yearly Financial results of the store.

Code:
```
WITH inv_det AS (
SELECT * FROM
  (
    SELECT
      s.storeid as sid,
      s.store_name AS storename,
      extract(year from id.Arrival_Date) as year,
      extract(month from id.Arrival_Date) as month,
      ii.type as type, count(id.item_copyid) itemid
    FROM  STORES s 
    left JOIN INVENTORY_DETAILS id ON s.storeid = id.dest_storeid
    JOIN INVENTORY_ITEMS ii ON id.item_copyid = ii.ITEM_COPYID
    where extract(year from id.Arrival_Date) = extract(year from SYSDATE)
    and id.STATUS = 'In Stock'
    group by s.storeid,
    s.store_name,
    extract(year from id.Arrival_Date),
    extract(month from id.Arrival_Date),
    ii.type
  )
  PIVOT
  (
    SUM(itemid)  
    for TYPE in ('BOOK' "book",'dvd' "dvd",'game' "game") 

  )
)
SELECT
  inv_det.sid as "STORE ID",
  inv_det.storename as "Store Name",
  inv_det.year,
  inv_det.month,
  coalesce(inv_det."book",0) as "Total Books", 
  coalesce(inv_det."dvd",0) as "Total DVD",
  coalesce(inv_det."game",0) as "Total Games",
  coalesce(inv_det."book",0)+coalesce(inv_det."dvd",0)+coalesce(inv_det."game",0) as "Total Available Inventory"
 
FROM inv_det
order by inv_det.sid
```

![Inventory Details](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/inventory_details.png)

### Query 10: 
The below query explains the details of all the employees hired in each store based on their skills.

Code:
```
With a as(
  select distinct emp.empID as empid, stores.storeid, a.skill_name 
  from Employees emp join applicant_skills a on emp.applicantID=a.applicantID
  join shifts on emp.empid=shifts.empid
  join stores on shifts.storeid=stores.storeid
  where exists (select ApplicantID from Applicants a where a.applicantID=emp.applicantID)
  order by emp.empid
),
b as (
select a.storeid as storeid, a.skill_name as skill_name, a.empid as emp_id
    from a
    group by a.storeid, a.skill_name, a.empid
    order by a.storeid)
Select * from (
    Select storeid, skill_name, emp_id
    from b
)SkillTable
PIVOT
    (
     count(emp_id)
     FOR Skill_name in('Communication','Computer Literate','Data Entry Expert','Industrious','Decision Making','Operations Management',
     'Customer Service','Motivating','Instrument Expert')
    )Skill_Pivot_table
order by storeid;
```

![Employee Details](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/employee_details.png)


### Query 11:
Bookman’s also needs to know the month’s and year’s ranking to find out their bestseller. This query gives the month's ranking and year's ranking of items based on the number of copies sold.

Code:
```
with month_det as 
(
  select to_char(to_date(m,'MM'),'month') as "Month",
  itmid as "Item Id", title as "Item Title",type as "Item Type",copycount as "Copies sold in the month",
  case
    when top_charts = 1 then 'Month Bestseller ranked 1'
    when top_charts = 2 then 'Month Bestseller ranked 2'
    when top_charts = 3 then 'Month Bestseller ranked 3'
    when top_charts = 4 then 'Month Bestseller ranked 4'
    when top_charts = 5 then 'Month Bestseller ranked 5'
    when top_charts = 6 then 'Month Bestseller ranked 6'
    when top_charts = 7 then 'Month Bestseller ranked 7'
    when top_charts = 8 then 'Month Bestseller ranked 8'
    when top_charts = 9 then 'Month Bestseller ranked 9'
    when top_charts = 10 then 'Month Bestseller ranked 10'
  end as "Month's picks"
  from
  (
    select extract(month from so.sale_date) m,
    extract(year from so.sale_date) y,
    ii.itemid itmid,
    i.title title,
    i.item_type type, 
    count(su.item_copyid) copycount,
    DENSE_RANK() over (partition by i.ITEM_TYPE,extract(month from so.sale_date ) order by count(su.item_copyid) desc) top_charts
    from sale_units su
    join inventory_items ii on su.item_copyid = ii.item_copyid
    join items i on i.itemid = ii.itemid
    join sale_orders so on so.sale_orderid = su.sale_orderid
    where extract(year from so.sale_date) = extract(year from SYSDATE)
    group by ii.itemid,i.title,i.item_type, extract(month from so.sale_date),extract(year from so.sale_date)
  )
  where top_charts < 10
  ),

year_det as 
(
  select extract(year from so.sale_date) y,ii.itemid itmid,i.title title,i.item_type type, 
  count(su.item_copyid) copycount,
  DENSE_RANK() over (partition by ITEM_TYPE,extract(year from so.sale_date ) order by count(su.item_copyid) desc) top_charts
  from sale_units su
  join inventory_items ii on su.item_copyid = ii.item_copyid
  join items i on i.itemid = ii.itemid
  join sale_orders so on so.sale_orderid = su.sale_orderid
  where extract(year from so.sale_date) = extract(year from SYSDATE)
  group by ii.itemid,i.title,i.item_type,extract(year from so.sale_date)
)

select month_det.* , year_det.top_charts as "Year's bestselling rank"
from month_det
join year_det on month_det."Item Id" = year_det.itmid;
```
![Most popular items](https://github.com/Abhilasha13/Bookstore_Database/blob/main/query_images/popular_items.png)
