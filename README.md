# 🚕 OLA Ride-Sharing SQL Analytics Dashboard 📊

> A deep-dive SQL-based analytics project for understanding Ola's ride patterns, cancellations, and customer behavior.

---

## 🧠 Project Overview
This project focuses on creating SQL views to analyze key operational and customer metrics from Ola's ride-sharing data. It highlights user preferences, booking trends, cancellation reasons, and revenue insights to support strategic decision-making.

---

## 🔧 Tech Stack & Tools

- **Database:** MySQL
- **Languages:** SQL
- **Tools:** MySQL Workbench, VS Code, GitHub

---

## 🗃️ Database Schema
```sql
CREATE TABLE bookings (
    Booking_ID INT,
    Customer_ID INT,
    Vehicle_Type VARCHAR(50),
    Booking_Status VARCHAR(50),
    Ride_Distance FLOAT,
    Driver_Ratings FLOAT,
    Customer_Rating FLOAT,
    Payment_Method VARCHAR(50),
    Booking_Value DECIMAL(10,2),
    cancelled_Rides_by_Driver VARCHAR(100),
    Incomplete_Rides VARCHAR(5),
    Incomplete_Rides_Reason VARCHAR(255)
);
```

---

## 📊 Analysis Features (SQL Views)

### 1. ✅ Successful Bookings
```sql
CREATE VIEW Successful_Bookings AS
SELECT * FROM bookings
WHERE Booking_Status = 'Success';
```
> Retrieves all bookings marked as successful.

### 2. 📏 Avg Ride Distance by Vehicle Type
```sql
CREATE VIEW ride_distance_for_each_vehicle AS
SELECT Vehicle_Type, AVG(Ride_Distance) AS avg_distance
FROM bookings
GROUP BY Vehicle_Type;
```
> Calculates average ride distance for each vehicle type.

### 3. ❌ Cancelled Rides by Customers
```sql
CREATE VIEW cancelled_rides_by_customers AS
SELECT COUNT(*) FROM bookings
WHERE Booking_Status = 'cancelled by Customer';
```
> Total number of rides cancelled by customers.

### 4. 🏆 Top 5 Frequent Customers
```sql
CREATE VIEW Top_5_Customers AS
SELECT Customer_ID, COUNT(Booking_ID) AS total_rides
FROM bookings
GROUP BY Customer_ID
ORDER BY total_rides DESC
LIMIT 5;
```
> Identifies the top 5 customers by number of rides.

### 5. 🚗 Driver Cancellations - Personal & Car Issues
```sql
CREATE VIEW Rides_cancelled_by_Drivers_P_C_Issues AS
SELECT COUNT(*) FROM bookings
WHERE cancelled_Rides_by_Driver = 'Personal & Car related issue';
```
> Number of rides cancelled by drivers due to personal or car issues.

### 6. ⭐ Max/Min Driver Ratings for Prime Sedan
```sql
CREATE VIEW Max_Min_Driver_Rating AS
SELECT MAX(Driver_Ratings) AS max_rating,
       MIN(Driver_Ratings) AS min_rating
FROM bookings
WHERE Vehicle_Type = 'Prime Sedan';
```
> Rating range for Prime Sedan rides.

### 7. 💳 UPI Payment Rides
```sql
CREATE VIEW UPI_Payment AS
SELECT * FROM bookings
WHERE Payment_Method = 'UPI';
```
> Retrieves all rides where UPI was the payment method.

### 8. 🌟 Avg Customer Rating by Vehicle
```sql
CREATE VIEW AVG_Cust_Rating AS
SELECT Vehicle_Type, AVG(Customer_Rating) AS avg_customer_rating
FROM bookings
GROUP BY Vehicle_Type;
```
> Average customer rating segmented by vehicle type.

### 9. 💰 Total Value of Successful Rides
```sql
CREATE VIEW total_successful_ride_value AS
SELECT SUM(Booking_Value) AS total_successful_ride_value
FROM bookings
WHERE Booking_Status = 'Success';
```
> Revenue from successfully completed rides.

### 10. 📉 Incomplete Rides & Reasons
```sql
CREATE VIEW Incomplete_Rides_Reason AS
SELECT Booking_ID, Incomplete_Rides_Reason
FROM bookings
WHERE Incomplete_Rides = 'Yes';
```
> Shows all incomplete rides with their respective reasons.

---

## 🔍 Key Insights

- UPI is a popular payment method among riders.
- Prime Sedan has wide rating variation, indicating inconsistent driver performance.
- A significant number of rides were cancelled by drivers due to personal and vehicle issues.
- Certain customers are highly loyal with 50+ bookings each.
- Customer ratings vary significantly across vehicle types.

---

## 💡 Strategic Recommendations

1. Improve driver reliability by addressing personal/car issue cancellations.
2. Offer incentives to top loyal customers.
3. Standardize service quality in Prime Sedan category.
4. Promote UPI payment through discounts or cashback.
5. Analyze incomplete ride reasons for route/network improvement.
6. Create customer satisfaction dashboards by vehicle category.
7. Launch customer re-engagement campaigns post-cancellation.

---

## 🚀 Installation Instructions
```sql
CREATE DATABASE Ola;
USE Ola;
-- Then execute all CREATE VIEW scripts above
```
> Ensure MySQL is installed and running.

---

## 🔧 Further Development Suggestions

- Integrate real-time ride booking data via API.
- Add customer demographics and driver profiles.
- Visualize insights using Tableau or Power BI.
- Automate email reports for key KPIs.
- Predict cancellations using ML models.

---

## 👨‍💻 Author & License

**Author:** Navanil Das  
📧 navanildas2702@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/navanil-das-a67836166/)  

📄 **License:** MIT

---
