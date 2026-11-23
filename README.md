# Laundry Hub

Laundry Hub is a web system that brings many independent laundries, their customers and a shared pool of delivery drivers into one platform. A customer chooses a laundry, orders online and follows the order until the clothes are back. A laundry owner registers the laundry and manages prices, staff and orders. Drivers register once and take pickup and delivery jobs from any laundry. An administrator approves new laundries and drivers.

The project is written in **plain HTML only** (no CSS, no JavaScript, no backend). Every page shows fixed sample data, so the full workflow of the system can be viewed and discussed in a browser.

## Contents

1. [Roles](#1-roles)
2. [How the system works](#2-how-the-system-works)
3. [Pages](#3-pages)
4. [Project structure](#4-project-structure)
5. [Running the project](#5-running-the-project)
6. [Sample data](#6-sample-data)
7. [Demonstration walkthrough](#7-demonstration-walkthrough)
8. [Business rules](#8-business-rules)
9. [Technology and scope](#9-technology-and-scope)
10. [Future development](#10-future-development)
11. [Team responsibilities](#11-team-responsibilities)
12. [Version history](#12-version-history)

---

## 1. Roles

| Role | Joins by | Main tasks |
|---|---|---|
| Customer | Registering | Browses laundries, compares prices, places orders, tracks orders, rates laundries |
| Laundry owner | Registering a laundry (approved by the admin) | Maintains the laundry profile, prices and fees, adds shopkeepers, accepts or rejects orders, follows deliveries, reads reports |
| Shopkeeper | Added by the owner | Registers walk-in orders, updates order status, hands over clothes and records payment |
| Driver | Registering (approved by the admin) | Takes pickup and delivery jobs from any laundry, updates job state, records money collected, sees earnings |
| Admin | Built into the platform | Approves or rejects laundries and drivers, suspends users |

A laundry has its own prices, delivery fees, shopkeepers and orders. A driver does **not** belong to a laundry. Drivers work for the whole platform, so one driver can work for several laundries on the same day.

## 2. How the system works

### 2.1 Joining the platform

- **Customers** register with name, phone number, area and address, then log in.
- **Laundries** register the owner and the laundry (area, address, opening hours, pickup and delivery fees). The laundry appears in the customer list after the admin approves it.
- **Drivers** register with personal details, ID number, area and vehicle. The admin checks the ID number and approves the account. Only approved drivers see the job board.
- **Shopkeepers** are created by the laundry owner on the Staff page.

### 2.2 Order lifecycle

An order passes through these statuses:

| Status | Meaning |
|---|---|
| Pending | The customer sent the order. The laundry has not answered yet |
| Accepted | The owner accepted the order |
| Rejected | The owner rejected the order and gave a reason |
| Received | The clothes arrived at the laundry (brought by the customer or by a driver) |
| Washing | The clothes are being washed |
| Finished | Washing is done |
| Ready for collection | The clothes wait at the shop for the customer or for a driver |
| Collected / Delivered | The customer has the clothes and the payment is recorded |

If an order is late, the shopkeeper records a delay reason (no electricity, water problem, machine problem or other) and a new estimated ready date.

### 2.3 Pickup and delivery jobs

Every pickup and every delivery is a **job** on a shared job board.

1. The owner accepts an order that includes pickup. A pickup job is posted to the job board.
2. When the shopkeeper hands over an order marked for delivery, a delivery job is posted.
3. Any approved driver can accept a job. The first driver to accept gets it.
4. The driver updates the job: accepted, picked up, on the way, delivered. If the customer is not available, the job returns to the job board.
5. After a delivery the driver gives the order money to the laundry and keeps the delivery fee.
6. The owner sees the job, the driver's name and the driver's phone number on the Deliveries page. The customer sees the same driver information on the tracking page.

Job states: **posted**, **accepted**, **picked up**, **on the way**, **delivered**, **cancelled**.

### 2.4 Fees and payment

- Each laundry sets a **pickup fee** and a **delivery fee** (Bereket Laundry: ETB 50 and ETB 100).
- The fee of a job is the driver's earning.
- Accepted payment methods: cash, Telebirr and bank transfer.
- Partial payments are allowed. The system shows the remaining balance.
- Walk-in customers pay the shopkeeper at hand over. Delivery customers pay the driver, who records the amount.
- Currency: Ethiopian birr (ETB).

## 3. Pages

The project has **34 pages**.

### Public (root folder)

| File | Purpose |
|---|---|
| `index.html` | Introduction to the system, how it works, links to register |
| `login.html` | One login form for each of the five roles |
| `register-customer.html` | Customer registration |
| `register-laundry.html` | Laundry owner and laundry registration |
| `register-driver.html` | Driver registration |

### Customer (`customer/`)

| File | Purpose |
|---|---|
| `laundries.html` | List of approved laundries with search by name, area and delivery |
| `laundry-detail.html` | Laundry information, services, prices, fees and reviews |
| `place-order.html` | Choose clothes, pickup or drop-off, collect or delivery |
| `order-confirmation.html` | Summary of the order that was sent |
| `my-orders.html` | All orders of the customer |
| `order-tracking.html` | Progress of one order, step by step |
| `rate-laundry.html` | Rating and comment for a collected order |

### Owner (`owner/`)

| File | Purpose |
|---|---|
| `dashboard.html` | Summary of requests, orders, deliveries and unpaid balance |
| `order-requests.html` | Accept or reject new online orders |
| `deliveries.html` | Pickup and delivery jobs of the laundry and the drivers who accepted them |
| `prices.html` | Service prices, active or inactive services, pickup and delivery fees |
| `staff.html` | List and creation of shopkeepers |
| `laundry-profile.html` | Name, phone, area, address, hours, description |
| `reports.html` | Orders, income and unpaid orders by day or month |

### Shopkeeper (`shop/`)

| File | Purpose |
|---|---|
| `dashboard.html` | Pending orders grouped by status |
| `new-order.html` | Register a walk-in order |
| `receipt.html` | Receipt of a registered order |
| `search-order.html` | Find an order by order number or phone number |
| `update-status.html` | Change the status, record a delay, see the status history |
| `handover.html` | Record payment and hand over the clothes |

### Driver (`driver/`)

| File | Purpose |
|---|---|
| `dashboard.html` | Summary and the jobs the driver accepted |
| `available-jobs.html` | Job board with jobs from all laundries, filtered by area and type |
| `job-details.html` | Pickup address, delivery address, order and money to collect |
| `update-job.html` | Update the job state and record the money collected |
| `history.html` | Finished jobs and total earnings |

### Admin (`admin/`)

| File | Purpose |
|---|---|
| `dashboard.html` | Platform totals and items that wait for approval |
| `laundries.html` | Approve, reject or suspend laundries |
| `drivers.html` | Approve, reject or suspend drivers |
| `users.html` | List of all users with role filter |

## 4. Project structure

```
laundry-hub/
├── index.html
├── login.html
├── register-customer.html
├── register-laundry.html
├── register-driver.html
├── customer/
│   ├── laundries.html
│   ├── laundry-detail.html
│   ├── place-order.html
│   ├── order-confirmation.html
│   ├── my-orders.html
│   ├── order-tracking.html
│   └── rate-laundry.html
├── owner/
│   ├── dashboard.html
│   ├── order-requests.html
│   ├── deliveries.html
│   ├── prices.html
│   ├── staff.html
│   ├── laundry-profile.html
│   └── reports.html
├── shop/
│   ├── dashboard.html
│   ├── new-order.html
│   ├── receipt.html
│   ├── search-order.html
│   ├── update-status.html
│   └── handover.html
├── driver/
│   ├── dashboard.html
│   ├── available-jobs.html
│   ├── job-details.html
│   ├── update-job.html
│   └── history.html
├── admin/
│   ├── dashboard.html
│   ├── laundries.html
│   ├── drivers.html
│   └── users.html
└── README.md
```

Folders are named after roles. Every page has the same layout: header, navigation menu of the role, main content and footer. The menu links use relative paths, so the folder can be moved or opened from any location.

## 5. Running the project

1. Unzip the project.
2. Open `index.html` in any web browser. No server or installation is needed.
3. Use the menu of each page to move through the system.
4. On `login.html`, any username and password are accepted. The button of a role opens the first page of that role.

## 6. Sample data

All pages use the same data so the system stays consistent.

**Laundries**

| Laundry | Area | Hours | Pickup / delivery fee | State |
|---|---|---|---|---|
| Bereket Laundry | Bole | 07:30 - 19:00 | ETB 50 / ETB 100 | Approved |
| Sheba Clean | Piassa | 08:00 - 20:00 | ETB 40 / ETB 80 | Approved |
| Addis Fresh | CMC | 08:00 - 18:00 | No delivery | Approved |
| Megenagna Quick Wash | Megenagna | - | - | Waiting for approval |

**Bereket Laundry prices (ETB):** Shirt 40, Trouser 60, Dress 80, Suit 250, Blanket 150. Towel (50) is inactive.

**People**

| Role | Name |
|---|---|
| Customer | Abebe Kebede (signed in on customer pages) |
| Owner | Bereket Tadesse |
| Shopkeepers | Hirut Alemayehu, Tadesse Bekele |
| Drivers | Mulugeta Tesfaye (signed in on driver pages), Samuel Girma. Kebede Alemu is waiting for approval |

**Orders at Bereket Laundry**

| Order | Customer | Status | Total (ETB) |
|---|---|---|---|
| ORD-0001 | Abebe Kebede | Received | 240 |
| ORD-0002 | Sara Tesfaye | Washing | 310 |
| ORD-0003 | Dawit Alemu | Ready for collection | 200 |
| ORD-0004 | Hana Girma | Finished | 500 |
| ORD-0005 | Kidus Bekele | Collected (paid cash) | 120 |
| ORD-0006 | Meron Haile | Ready, delivery job accepted by a driver | 260 |
| ORD-0008 | Abebe Kebede | Pending, with pickup and delivery | 460 |
| ORD-0009 | Tigist Bekele | Accepted, pickup job accepted by a driver | 250 |
| ORD-0010 | Rahel Mulu | Pending, drop-off | 180 |

Other orders: ORD-0007 (Sheba Clean, collected) and ORD-0011 (Sheba Clean, delivery job on the job board). Unpaid balance at Bereket Laundry: ETB 1510.

## 7. Demonstration walkthrough

**Customer orders with pickup and delivery**
1. `login.html` - log in as customer.
2. `customer/laundries.html` - choose Bereket Laundry.
3. `customer/laundry-detail.html` - read prices and fees, press the order button.
4. `customer/place-order.html` - enter the clothes, select pickup and delivery, send the order.
5. `customer/order-confirmation.html` and `customer/my-orders.html` - see the pending order.

**Owner accepts the order**
1. `owner/order-requests.html` - accept ORD-0008.
2. `owner/deliveries.html` - the pickup job is now on the job board.

**Driver takes the job**
1. `driver/available-jobs.html` - jobs from Bereket Laundry and Sheba Clean are listed together.
2. `driver/dashboard.html` - accepted jobs.
3. `driver/job-details.html` and `driver/update-job.html` - addresses, money to collect, state update.
4. `driver/history.html` - finished jobs and earnings.

**Shop works on the order**
1. `shop/dashboard.html` - orders by status.
2. `shop/update-status.html` - received, washing, finished, ready for collection; delay reason.
3. `shop/handover.html` - payment and hand over, collection or delivery.

**Administration**
1. `admin/laundries.html` and `admin/drivers.html` - approve a new laundry and a new driver.
2. `owner/reports.html` - daily and monthly orders, income and unpaid orders.

## 8. Business rules

- Phone numbers have 10 digits and start with 09.
- An order can be handed over only when its status is *Ready for collection*.
- A service marked inactive stays in the price list and cannot be chosen for new orders.
- A laundry or a driver becomes visible to the platform only after admin approval.
- A job is accepted by exactly one driver. The first driver to accept gets it. The owner can cancel a job that has no driver.
- The driver keeps the fee of the job and gives the order money to the laundry.
- If a customer is not available at delivery, the job returns to the job board.
- Search finds an order by order number or customer phone number.
- If no record exists, the page shows "Order not found" or "No records found for this period".

## 9. Technology and scope

- **HTML only.** The project contains no CSS and no JavaScript. Tables use the HTML `border`, `cellpadding` and `cellspacing` attributes so that data is readable.
- **Static pages.** There is no database and no server. Forms use the GET method and open the next page of the workflow. Nothing is saved, and totals are not calculated.
- **Semantic structure.** Each page uses `header`, `nav`, `main`, `section` and `footer`. Forms use `label`, `fieldset` and `legend`. Tables use `caption`, `thead`, `tbody` and `scope`.
- **Built-in validation.** Fields use HTML attributes such as `required`, `pattern`, `min` and `maxlength` for phone numbers, dates and quantities.
- **Language.** English. Currency ETB. Place names are from Addis Ababa.

## 10. Future development

- JavaScript for order totals, form checks and live filtering of the laundry list and job board.
- Backend and database. The main tables:

| Table | Main fields |
|---|---|
| `users` | id, name, phone, username, password hash, role, state |
| `laundries` | id, owner_id, name, area, address, opening_time, closing_time, pickup_fee, delivery_fee, state |
| `services` | id, laundry_id, name, price, state |
| `orders` | id, customer_id, laundry_id, status, estimated_ready_date, pickup, delivery, address, total |
| `order_items` | id, order_id, service_id, quantity, unit_price |
| `jobs` | id, order_id, type, driver_id, state, fee, scheduled_for |
| `payments` | id, order_id, job_id, method, amount, received_by, date |
| `status_history` | id, order_id, status, delay_reason, date |
| `reviews` | id, order_id, laundry_id, rating, comment |
| `drivers` | user_id, id_number, vehicle, plate, area, state |

- Real payments with Telebirr.
- A platform commission on delivery fees.
- Driver ratings, live map and notifications by SMS.

## 11. Team responsibilities

| Module | Folder | Responsible member |
|---|---|---|
| Public pages and customer | `/` and `customer/` | |
| Owner | `owner/` | |
| Shopkeeper | `shop/` | |
| Driver and admin | `driver/` and `admin/` | |

## 12. Version history

| Version | Content |
|---|---|
| Phase 1 | Single laundry: login, new order, receipt, search, update status, handover, prices, reports (9 pages) |
| Phase 2 | Multi-laundry platform with customers, laundry owners, platform drivers and admin (34 pages); the Phase 1 pages are in `shop/` and `owner/` |
