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

# 💾 การวิเคราะห์ข้อมูลด้วย SQL (SQLite)
## 📑 PIZZA SALES SQL QUERIES (SQLite)
### 💡 A. KPIs (Key Performance Indicators)
**🌻 เรามาเริ่มคำนวณตัวชี้วัดประสิทธิภาพหลักที่สำคัญต่อธุรกิจกันก่อนเลยจ้าาา 💰**

**1. Total Revenue (หารายได้รวมของออเดอร์พิซซ่าทั้งหมด)**
```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/total_revenue.jpg)

**2. Average Order Value ยอดเงินเฉลี่ยที่ลูกค้าใช้จ่ายต่อ 1 ออร์เดอร์**
```sql
SELECT ROUND(SUM(total_price) / COUNT(DISTINCT order_id),2) AS Avg_order_value FROM pizza_sales;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/avg_order_value.jpg)

**3. Total Pizzas Sold จำนวนพิซซ่าทั้งหมดที่ขายออกไป**
```sql
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/total_pizzas_sold.jpg)

**4. Total Orders นับจำนวนออร์เดอร์ที่ได้รับทั้งหมด**
```sql
SELECT COUNT(DISTINCT order_id) AS Total_orders FROM pizza_sales;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/total_orders.jpg)

**5. Average Pizzas Per Order จำนวนพิซซ่าเฉลี่ยต่อ 1 ออร์เดอร์**
```sql
SELECT SUM(quantity) / COUNT(DISTINCT order_id) AS Avg_pizzas_per_order FROM pizza_sales;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/avg_pizzas_per_order.jpg)

### 💡 B.Daily Trend for Total Orders
**🌻 ต้องการผลลัพธ์เป็นชื่อวันในสัปดาห์ (Monday, Tuesday) สำหรับแนวโน้มรายวัน (7 วัน)**
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
FROM pizza_sales
GROUP BY Day_of_week_name
ORDER BY Total_orders;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/daily-trend-for-total-orders.jpg)

### 💡 C.Hourly Trend for Orders
**🌻 สร้างแนวโน้มจำนวนออเดอร์รายชั่วโมงจากคอลัมน์ order_time เพื่อดูช่วงเวลาที่มีการสั่งซื้อมากที่สุด**
```sql
SELECT
    STRFTIME('%H', order_time) AS Order_Hour, -- ดึงชั่วโมงออกมา (00-23)
    COUNT(DISTINCT order_id)   AS Total_Orders
FROM pizza_sales
WHERE order_time IS NOT NULL -- กรองข้อมูลที่ order_time ไม่เป็น NULL
    AND order_time != ''   -- กรองข้อมูลที่ order_time ไม่เป็นค่าว่าง
GROUP BY Order_Hour
ORDER BY Order_Hour;
```

🍁 จากข้อมูลเราจะเห็นว่าเวลาที่มีจำนวนออเดอร์ค่อนข้างเยอะจะเป็นช่วงใกล้พักเที่ยงหรือช่วงเวลามื้ออาหารกลางวัน และอีกช่วงคือช่วงเย็น 16.00-19.00 น.

🍁 หากเราทราบช่วงเวลาที่มีออเดอร์จำนวนมากจะช่วยให้เราสามารถวางแผนการจัดเตรียมพนักงาน วัตถุดิบ และการจัดส่งล่วงหน้าได้อย่างมีประสิทธิภาพ

🍁 นอกจากนี้ยังสามารถใช้ข้อมูลนี้ในการวางแผนโปรโมชันหรือกิจกรรมการตลาดในช่วงเวลาที่เหมาะสมเพื่อเพิ่มยอดขายได้อีกด้วย
### 💡 D. % of Sales by Pizza Category
**🌻 คำนวณสัดส่วนเปอร์เซ็นต์ยอดขายตามหมวดหมู่พิซซ่า เพื่อทำความเข้าใจความนิยมของพิซซ่าแต่ละประเภท**

**🌻 เราจะใช้ Common Table Expressions (CTEs) เพื่อคำนวณรายได้ของแต่ละหมวดหมู่และรายได้รวมทั้งหมด ก่อนที่จะนำมาคำนวณหาเปอร์เซ็นต์**
```sql
WITH pizzaCategorySales  AS (
    SELECT
        pizza_category,
        SUM(total_price) AS category_revenue
    FROM pizza_sales
    GROUP BY pizza_category
),  totalSales           AS (
    SELECT
        SUM(total_price) AS Grand_Total_Revenue
    FROM pizza_sales
)

SELECT
    t1.pizza_category,
    t1.category_revenue,
    ROUND((t1.Category_Revenue * 100.0) / t2.Grand_Total_Revenue, 2) AS Percentage_of_Sales
FROM pizzaCategorySales AS t1, totalSales AS t2
ORDER BY Percentage_of_Sales DESC; 

```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/pizza_total_percentage.jpg)

### 💡 E. % of Sales by Pizza Size
**🌻 คำนวณสัดส่วนเปอร์เซ็นต์ยอดขายตามขนาดพิซซ่า เพื่อทำความเข้าใจความชอบของลูกค้าต่อขนาดต่างๆ**
```sql
  WITH sizeTotalSalse AS (
      SELECT 
          pizza_size,
          ROUND(SUM(total_price), 2) AS total_revenue_by_size
      FROM pizza_sales
      GROUP BY pizza_size
  ),  grandTotal  AS (
   SELECT 
     	SUM(total_price)  aS grand_total
   FROM pizza_sales
  )
  
  
  SELECT 
    t1.pizza_size,
    t1.total_revenue_by_size,
    ROUND((t1.total_revenue_by_size * 100.0) / grand_total, 2) AS percentage_of_total_salse
  FROM sizeTotalSalse AS t1, grandTotal AS t2
  ORDER BY percentage_of_total_salse DESC;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/total_rev_by_size_pizza.jpg)

🍁 จากข้อมูลพิซซ่าขนาดที่เป็นที่นิยมและมียอดขายมากที่สุดคือ ‘size L’ รองลงมาเป็น ‘size M’ ในขณะที่พิซซ่าขนาด ‘XXL’ มียอดสั่งน้อยที่สุด

### 💡 F. Total Pizzas Sold by Pizza Category
**🌻 ดูจำนวนพิซซ่าทั้งหมดที่ขายได้ในแต่ละหมวดหมู่พิซซ่า เพื่อเปรียบเทียบประสิทธิภาพการขาย**
```sql
SELECT 
    pizza_category,
    SUM(quantity)  AS Total_Quantity_Sold
FROM pizza_sales
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/pizza_classic.jpg)

🍁 หมวดหมู่พิซซ่าที่ขายดีที่สุดและมีปริมาณการขายมากที่สุดคือ ‘Classic’ สอดคล้องกับยอดขายรวม และหมวดหมู่ที่มีปริมาณการขายน้อยที่สุดคือ ‘Chicken’

### 💡 G. Top 5 Best Sellers by Total Pizzas Sold
**🌻 ค้นหา 5 อันดับพิซซ่าที่ขายดีที่สุด โดยอ้างอิงจากจำนวนพิซซ่าที่ขายได้ทั้งหมด**
```sql
SELECT 
    pizza_name,
    SUM(quantity)  AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
LIMIT 5;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/pizza_name_top5.jpg)

🍁 นี่คือรายชื่อ 5 อันดับพิซซ่าที่ได้รับความนิยมสูงสุดจากจำนวนที่ขายได้ ซึ่งสามารถนำไปใช้ในการวางแผนสต็อกสินค้าและการตลาดได้

### 💡 H. Bottom 5 Best Sellers by Total Pizzas Sold
**🌻 ค้นหา 5 อันดับพิซซ่าที่ขายได้น้อยที่สุด โดยอ้างอิงจากจำนวนพิซซ่าที่ขายได้ทั้งหมด**
```sql
SELECT 
    pizza_name,
    SUM(quantity)  AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold 
LIMIT 5;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/pizza_bottom_5.jpg)

🍁 นี่คือรายชื่อ 5 อันดับพิซซ่าที่ขายได้น้อยที่สุด ซึ่งอาจต้องพิจารณากลยุทธ์เพื่อปรับปรุงยอดขาย

----
## 🍕 ข้อเสนอแนะเชิงธุรกิจเพิ่มเติม
1. ใช้ข้อมูลแนวโน้มรายวันและรายชั่วโมงเพื่อจัดตารางพนักงานให้เหมาะสมกับช่วงเวลาที่มีออเดอร์หนาแน่นที่สุด เพื่อเพิ่มประสิทธิภาพการบริการและลดเวลาในการรอของลูกค้าเพื่อสร้างความประทับใจ หรือเพิ่มความพึงพอใจของลูกค้าให้กลับมาใช้บริการซ้ำ

2. เน้นการสต็อกวัตถุดิบสำหรับพิซซ่าหมวดหมู่ ‘Classic’ และขนาด ‘L’ ให้เพียงพอ เนื่องจากเป็นสินค้าที่ขายดีที่สุด และพิจารณาจัดโปรโมชันสำหรับพิซซ่าหมวดหมู่ ‘Chicken’ หรือขนาด ‘XXL’ เพื่อกระตุ้นยอดขาย หรืออาจพิจารณาปรับปรุงเมนูสำหรับสินค้าที่ขายน้อยที่สุด

3. ออกแบบโปรโมชันที่สอดคล้องกับพฤติกรรมการซื้อ เช่น จัดโปรโมชัน “Happy Hour” ในช่วงที่ยอดขายเริ่มสูงขึ้น เพื่อกระตุ้นยอดขายให้เพิ่มขึ้นไปอีก หรือจัดชุดคอมโบสำหรับขนาด ‘L’ หรือ ‘M’ ที่เป็นที่นิยม

----
✨🍫 Explore more of my work on my portfolio website: [https://datateathyme.wordpress.com](https://datateathyme.wordpress.com/2025/07/22/sql-supermarket-analytics-case-study/)
