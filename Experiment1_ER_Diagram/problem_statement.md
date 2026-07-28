# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1215" height="819" alt="image" src="https://github.com/user-attachments/assets/6899ef28-77c2-4570-929a-4b701deaf144" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member | member_id (PK), name, gender, dob, email                    | Represents gym members who register for programs.     |
| Program | program_id (PK), program_name, fee, duration, schedule                   |Represents the different fitness programs (e.g., Yoga, Zumba, Weight Training).       |
| Trainers | trainer_id (PK), trainer_name, trainer_gender, trainer_phone, trainer_email, expertise                   | Stores trainer information (e.g., contact details, expertise).      |
| Sessions |session_id (PK), date, time, trainer_id (FK), program_id (FK)                    |Represents individual time-bound classes.       |
| Payment | payment_id (PK), amount, payment_type, payment_date, member_id (FK), program_id (FK)                  | Records payments made by members for specific programs.      |
|Attendance|attendance_id (PK), status, session_id (FK), trainer_id (FK)|Tracks attendance of members in specific sessions.|

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|  enrolls_in           |    M:N        | Member (Total), Program (Partial)              |  A member can enroll in multiple programs; a program can have many members.     |
|   leads           |   1:M         |Program (Total), Trainer (Partial)| Each program is led by one trainer, but a trainer may lead multiple programs.      |
|   registers           |  M:N          |  Both Partial             | A member can register for many sessions, and each session can have many members.      |
|   includes           |  1:M          |   Program (Total), Session (Total)            | A program includes multiple sessions, but each session belongs to only one program.      |
|   has           | 1:M           | Program (Total), Payment (Total)              |A program can have many payments; each payment belongs to one program.       |
|tracks|1:M|Payment (Total), Session (Partial)|Payments are linked to sessions attended by members.|

### Assumptions
- A member must enroll in at least one program.
- A program must be led by at least one trainer.
- Payments are tied to members and programs (not to trainers directly).

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="1614" height="975" alt="image" src="https://github.com/user-attachments/assets/89a26444-1ced-4ef3-8c79-aa634e313b51" />


### Entities and Attributes

| Entity       | Attributes (PK)                                                                 | Notes                 |
| ------------ | ------------------------------------------------------------------------------- | --------------------- |
| Member       | member_id (PK), name, phone, email                                              | Stores member details |
| Book         | book_id (PK), isbn, title, author, category, publisher, publication_year        | Stores book details   |
| Loan         | loan_id (PK), loan_date, due_date, return_date, status                          | Book loan details     |
| Fine         | fine_id (PK), amount, paid_status, paid_date                                    | Fine details          |
| Event        | event_id (PK), event_name, event_date, event_time, event_type, description, fee | Library events        |
| Speaker      | speaker_id (PK), name, expertise, contact_no                                    | Event speaker details |
| Registration | registration_id (PK), registration_date, status                                 | Event registration    |
| Book_Author  | author_id (PK), book_id, author_name, author_type                               | Author information    |
| Room         | room_id (PK), room_name, room_type, capacity, location                          | Event room details    |


### Relationships and Constraints

| Relationship                | Cardinality | Participation | Notes                            |
| --------------------------- | ----------- | ------------- | -------------------------------- |
| Member borrows Book         | M:N         | Total         | Members borrow books             |
| Loan has Fine               | 1:1         | Partial       | Fine issued if overdue           |
| Member registers Event      | 1:M         | Partial       | Member registers for events      |
| Event has Speaker           | 1:M         | Total         | Event may have multiple speakers |
| Event held in Room          | M:1         | Total         | Event is conducted in one room   |
| Book written by Book_Author | 1:M         | Total         | Book may have multiple authors   |
| Registration booked in Room | M:1         | Total         | Registration assigned to a room  |


### Assumptions
- Each member has a unique member_id.
- A book can have multiple authors.
- A fine is generated only for overdue loans.
- Each event is conducted in one room.
- A member can register for multiple events. 

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="1522" height="712" alt="reservedbms drawio (1)" src="https://github.com/user-attachments/assets/2ce6ee0e-9b02-4bb8-b36a-06415a58d348" />


### Entities and Attributes

| Entity      | Attributes (PK)                                                         | Notes                     |
| ----------- | ----------------------------------------------------------------------- | ------------------------- |
| Customer    | customer_id (PK), name, phone_number, email_id                          | Stores customer details   |
| Reservation | reservation_id (PK), date, time, reservation_type, no_of_guests         | Table reservation details |
| Waiter      | waiter_id (PK), name, phone, section                                    | Waiter details            |
| Order       | order_id (PK), order_time, special_request                              | Customer order details    |
| Order Item  | order_item_id (PK), quantity, unit_price, sub_total                     | Ordered dish details      |
| Dish        | dish_id (PK), dish_name, price                                          | Restaurant menu items     |
| Category    | category_id (PK), category_name, description                            | Dish categories           |
| Bill        | bill_id (PK), bill_date, food_amount, tax, service_charge, total_amount | Billing details           |


### Relationships and Constraints

| Relationship                 | Cardinality | Participation | Notes                                   |
| ---------------------------- | ----------- | ------------- | --------------------------------------- |
| Customer makes Reservation   | 1:M         | Total         | Customer can make multiple reservations |
| Reservation served by Waiter | M:1         | Total         | One waiter serves many reservations     |
| Reservation has Order        | 1:1         | Total         | Each reservation has one order          |
| Order contains Order Item    | 1:M         | Total         | One order contains multiple items       |
| Order Item includes Dish     | M:1         | Total         | Each order item refers to one dish      |
| Category classifies Dish     | 1:M         | Total         | One category contains many dishes       |
| Reservation generates Bill   | 1:1         | Total         | One reservation generates one bill      |


### Assumptions
- Each customer has a unique customer_id.
- A customer can make multiple reservations.
- Every reservation is served by one waiter.
- Each reservation generates one bill.
- A dish belongs to one category.
- An order can contain multiple order items.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
