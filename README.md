#  Bookstore Relational Database

This project is a fully normalized SQL-based relational database system designed to manage core operations of a bookstore. It models everything from books and authors to customers, orders, and shipping, while implementing best practices in database design, security, and scalability.

---

## Project Overview

The **Bookstore Database** handles:

- Book inventory and languages
- Author relationships (including co-authors)
- Publishers and book pricing
- Customer accounts and multiple address support
- Order processing, shipping methods, and order status tracking
- User roles and access controls for security

This makes it perfect for both learning and deploying a real-world inventory and sales system for a small-to-medium bookstore.

---

## Schema Highlights

The database includes the following core tables:

- `book`, `book_author`, `author`
- `publisher`, `book_language`
- `customer`, `customer_address`, `address`, `country`, `address_status`
- `cust_order`, `order_line`, `order_status`, `order_history`
- `shipping_method`
- Role-based users for `staff`, `analyst`, and `admin`

All foreign keys are in place to ensure referential integrity, and the schema is normalized to at least 3NF (Third Normal Form).



## User Roles

- `bookstore_admin`: Full access (DDL + DML)
- `bookstore_staff`: Limited access (insert/update/select)
- `bookstore_analyst`: Read-only access for reporting and analytics

This access control ensures data safety while supporting role-based workflows.

---

## Sample Data

Pre-filled with:

- 4 languages, 3 publishers, and 4 authors
- 4 sample books (including a co-authored one)
- 3 customers and multi-address entries
- 3 customer orders with varying statuses
- Complete order history records for traceability

---

## Example Queries

```sql
-- List books with their authors
SELECT b.title, a.name AS author
FROM book b
JOIN book_author ba ON b.book_id = ba.book_id
JOIN author a ON ba.author_id = a.author_id;

-- Calculate total per order
SELECT o.order_id, c.full_name, SUM(ol.quantity * ol.price) AS total
FROM cust_order o
JOIN customer c ON o.customer_id = c.customer_id
JOIN order_line ol ON o.order_id = ol.order_id
GROUP BY o.order_id, c.full_name;
