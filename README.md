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
GROUP BY ITEM_TYPE),

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
GROUP BY ITEM_TYPE)

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


