# SQL Portfolio Project: Pizza Sales🍕
### 🌻 Portfolio | Data Analyst Portfolio Project | SQL Project | For Beginners
## 🍕 ภาพรวมโปรเจกต์
โปรเจกต์นี้เป็นการวิเคราะห์ข้อมูลยอดขายพิซซ่าโดยใช้ SQL (SQLite) เพื่อดึงข้อมูลเชิงลึกและแนวโน้มที่สำคัญทางธุรกิจ ซึ่งจะเป็นประโยชน์ต่อการตัดสินใจและปรับปรุงกลยุทธ์การดำเนินงาน

เราจะมุ่งเน้นการคำนวณตัวชี้วัดประสิทธิภาพหลัก (Key Performance Indicators – KPIs) และการวิเคราะห์แนวโน้มต่างๆ เพื่อตอบคำถามทางธุรกิจที่สำคัญ
## เครื่องมือที่ใช้
- 🛠 SQL (SQLite)

## 📑 PROBLEM STATEMENT : สิ่งที่ต้องการวิเคราะห์
เราต้องการวิเคราะห์ข้อมูลยอดขายพิซซ่าเพื่อทำความเข้าใจประสิทธิภาพของธุรกิจ ของเรามากขึ้น โดยการคำนวณและวิเคราะห์ข้อมูลเพื่อหาข้อมูลเชิงลึกจากข้อมูลต่อไปนี้

เพื่อช่วยให้เราสามารถประเมินผลการดำเนินงานในปัจจุบันและระบุโอกาสการปรับปรุงร้านหรือการบริการของเราในอนาคตให้ดียิ่งขึ้นได้
## 💡 KPIs REQUIREMENT (Key Performance Indicators)
เราต้องการวิเคราะห์ key indicators หรือตัวชี้วัดสำคัญจากข้อมูลยอดขายพิซซ่า เพื่อให้เข้าใจประสิทธิภาพธุรกิจของเรามากขึ้น โดยเฉพาะอย่างยิ่ง เราจะคำนวณข้อมูลต่อไปนี้

1. Total Revenue (รายได้รวม): ราคารวมของออเดอร์พิซซ่าทั้งหมด

2. Average Order Value (มูลค่าเฉลี่ยต่อออเดอร์): ยอดเงินเฉลี่ยที่ลูกค้าใช้จ่ายต่อ 1 ออเดอร์ (คำนวณจาก รายได้รวม หารด้วย จำนวนออเดอร์ทั้งหมด)

3. Total Pizzas Sold (จำนวนพิซซ่าที่ขายได้ทั้งหมด): ปริมาณพิซซ่าทั้งหมดที่ขายออกไป

4. Total Orders (จำนวนออเดอร์ทั้งหมด): จำนวนออเดอร์ที่ได้รับทั้งหมด

5. Average Pizzas Per Order (จำนวนพิซซ่าเฉลี่ยต่อออเดอร์): จำนวนพิซซ่าเฉลี่ยใน 1 ออเดอร์ (คำนวณจาก จำนวนพิซซ่าที่ขายได้ทั้งหมด หารด้วย จำนวนออเดอร์ทั้งหมด)

## 📈 แนวโน้มและสัดส่วน (Trends & Proportions)

1. Daily Trend for Total Orders: แนวโน้มจำนวนออเดอร์ทั้งหมดในแต่ละวัน

2. Hourly Trend for Total Orders: แนวโน้มจำนวนออเดอร์ทั้งหมดในแต่ละชั่วโมง

3. Percentage of Sales by Pizza Category: สัดส่วนยอดขายของพิซซ่าแต่ละประเภท

4. Percentage of Sales by Pizza Size: สัดส่วนยอดขายของพิซซ่าแต่ละขนาด

5. Total Pizzas Sold by Pizza Category: จำนวนพิซซ่าที่ขายได้ทั้งหมดในแต่ละหมวดหมู่

6. Top 5 Best Sellers by Total Pizzas Sold: 5 อันดับพิซซ่าที่ขายดีที่สุดตามจำนวนที่ขายได้

7. Bottom 5 Worst Sellers by Total Pizzas Sold: 5 อันดับพิซซ่าที่ขายได้น้อยที่สุด

## 📑 PIZZA SALES SQL QUERIES (SQLite)
### 💡 A.KPI’s
**1. Total Revenue หารายได้รวมของออร์เดอร์พิซซ่าทั้งหมด**
```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
```
**2. Average Order Value ยอดเงินเฉลี่ยที่ลูกค้าใช้จ่ายต่อ 1 ออร์เดอร์**
```sql
SELECT ROUND(SUM(total_price) / COUNT(DISTINCT order_id),2) AS Avg_order_value FROM pizza_sales;
```
**3. Total Pizzas Sold จำนวนพิซซ่าทั้งหมดที่ขายออกไป**
```sql
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
```
**4. Total Orders นับจำนวนออร์เดอร์ที่ได้รับทั้งหมด**
```sql
SELECT COUNT(DISTINCT order_id) AS Total_orders FROM pizza_sales;
```
**5. Average Pizzas Per Order จำนวนพิซซ่าเฉลี่ยต่อ 1 ออร์เดอร์**
```sql
SELECT SUM(quantity) / COUNT(DISTINCT order_id) AS Avg_pizzas_per_order FROM pizza_sales;
```
### 💡 B.Daily Trend for Total Orders
**ต้องการผลลัพธ์เป็นชื่อวันในสัปดาห์ (Monday, Tuesday, ...) สำหรับแนวโน้มรายวัน (7 วัน)**
```sql
SELECT
     STRFTIME('%w', SUBSTR(order_date, 7, 4) || '-' || SUBSTR(order_date, 4, 2) || '-' || SUBSTR(order_date, 1, 2)) AS Day_of_week_number,
     CASE STRFTIME('%w', SUBSTR(order_date, 7, 4) || '-' || SUBSTR(order_date, 4, 2) || '-' || SUBSTR(order_date, 1, 2))
        WHEN '0' THEN 'Sunday'
        WHEN '1' THEN 'Monday'
        WHEN '2' THEN 'Tuesday'
        WHEN '3' THEN 'Wednesday'
        WHEN '4' THEN 'Thursday'
        WHEN '5' THEN 'Friday'
        WHEN '6' THEN 'Saturday'
     END AS Day_of_week_name,
     COUNT (DISTINCT order_id) as Total_orders     
FROM
    pizza_sales
GROUP BY
    Day_of_week_name
ORDER BY
    Total_orders;
```
### 💡 C.Hourly Trend for Orders
**สร้าง แนวโน้มออร์เดอร์รายชั่วโมง จากคอลัมน์ order_time**
```sql
SELECT
    STRFTIME('%H', order_time) AS Order_Hour, -- ดึงชั่วโมงออกมา (00-23)
    COUNT(DISTINCT order_id) AS Total_Orders
FROM
    pizza_sales
WHERE
    order_time IS NOT NULL -- กรองข้อมูลที่ order_time ไม่เป็น NULL
    AND order_time != ''   -- กรองข้อมูลที่ order_time ไม่เป็นค่าว่าง
GROUP BY
    Order_Hour
ORDER BY
    Order_Hour;
```
### 💡 D. % of Sales by Pizza Category
**คำนวณเปอร์เซ็นต์ยอดขายตามหมวดหมู่พิซซ่า**
```sql
WITH PizzaCategorySales AS (
    SELECT
        pizza_category,
        SUM(total_price) AS Category_Revenue
    FROM
        pizza_sales
    WHERE
        pizza_category IS NOT NULL AND pizza_category != '' -- กรองข้อมูลที่หมวดหมู่ไม่ใช่ค่าว่าง
    GROUP BY
        pizza_category
),
TotalSales AS (
    SELECT
        SUM(total_price) AS Grand_Total_Revenue
    FROM
        pizza_sales
    WHERE
        pizza_category IS NOT NULL AND pizza_category != '' -- กรองข้อมูลที่หมวดหมู่ไม่ใช่ค่าว่าง
)
SELECT
    PCS.pizza_category,
    PCS.Category_Revenue,
    ROUND((PCS.Category_Revenue * 100.0) / TS.Grand_Total_Revenue, 2) AS Percentage_of_Sales
FROM
    PizzaCategorySales AS PCS,
    TotalSales AS TS
ORDER BY
    Percentage_of_Sales DESC; -- Order by percentage to see top categories
```
