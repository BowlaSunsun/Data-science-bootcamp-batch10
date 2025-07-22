# 🛍Case Study: SQL Supermarket Analytics 
## 🛒ภาพรวมโปรเจกต์

โปรเจกต์นี้เป็นการนำทักษะพื้นฐาน SQL มาประยุกต์ใช้ในการวิเคราะห์ข้อมูลยอดขายของซูเปอร์มาร์เก็ตที่เราจำลองขึ้นมา

เพื่อดึงข้อมูลเชิงลึกที่สำคัญ ช่วยให้ธุรกิจเข้าใจสถานการณ์ปัจจุบัน ระบุแนวโน้ม และทำความเข้าใจพฤติกรรมลูกค้า เพื่อนำไปสู่การตัดสินใจที่ขับเคลื่อนด้วยข้อมูล ได้อย่างมีประสิทธิภาพ
## 🚀เส้นทางของ Data Analyst วิเคราะห์ข้อมูลด้วย SQL
Data Analyst มักจะได้รับคำถามจากผู้บริหารหรือจากทีมที่เกี่ยวข้อง บ่อยครั้งว่า “ข้อมูลบอกอะไรเราบ้าง?”

**🛠 SQL** จึงเป็นอีกเครื่องมือสำคัญที่ช่วยเราตอบคำถามเหล่านั้น
## 👜คำถามทางธุรกิจที่พบบ่อยในการวิเคราะห์ข้อมูลซูเปอร์มาร์เก็ต
- ยอดขายและรายได้
  - ยอดขายรวมทั้งหมด (Total Sales)
  - รายได้เฉลี่ยต่อออร์เดอร์ (Average Order Value – AOV)
  - สินค้าขายดีที่สุด (Top-selling products)
  - หมวดหมู่สินค้าที่สร้างรายได้สูงสุด (Top-performing product categories)
  - แนวโน้มยอดขายรายวัน/รายสัปดาห์/รายเดือน (Daily/Weekly/Monthly sales trends)
  - ยอดขายตามสาขา (Sales by branch)
- พฤติกรรมลูกค้า
  - ประเภทลูกค้า (สมาชิก vs. ลูกค้าทั่วไป) และพฤติกรรมการซื้อ
  - ยอดใช้จ่ายเฉลี่ยของลูกค้าแต่ละประเภท
  - วิธีการชำระเงินที่นิยม
  - การจัดอันดับลูกค้าตามยอดซื้อ (Top customers by spending)
- ประสิทธิภาพการดำเนินงาน
  - ช่วงเวลาที่ลูกค้าพลุกพล่านที่สุด
  - การประเมินประสิทธิภาพของสินค้า (เช่น กำไรต่อสินค้า)
## 💾แหล่งข้อมูล
เราใช้ชุดข้อมูล จำลอง(Mockup) ชื่อ **'supermarket_sales'** จำนวน 100 รายการ ข้อมูลประกอบด้วยรายละเอียดการซื้อขาย

เช่น รหัสบิล, ประเภทสินค้า, ราคา, ปริมาณ, ประเภทลูกค้า (สมาชิก/ทั่วไป), สาขา, วันที่, เวลา, วิธีชำระเงิน และคะแนนความพึงพอใจลูกค้า
## 🛠เครื่องมือที่ใช้
- [X] SQL (SQLite)
### 🌷 คำอธิบายคอลัมน์เพิ่มเติม
- cogs: ต้นทุนสินค้าที่ขาย (Cost Of Goods Sold) (ตัวเลขทศนิยม)
- gross_margin_percentage: เปอร์เซ็นต์กำไรขั้นต้น (ตัวเลขทศนิยม)
- gross_income: กำไรขั้นต้น (ตัวเลขทศนิยม คือ total - cogs)
- rating: คะแนนความพึงพอใจลูกค้า (ตัวเลขทศนิยม 1.0 – 10.0)

## 📝ตัวอย่างของ SQL Query และแนวทางแก้ปัญหา (เบื้องต้น)
### ปัญหาที่ 1: สถานะยอดขายโดยรวมเป็นอย่างไร? (ตัวชี้วัด – KPIs)
🌻 ธุรกิจต้องการการสรุปผลประกอบการอย่างรวดเร็ว โดยมีวัตถุประสงค์เพื่อทราบยอดขายรวม จำนวนออเดอร์ที่เกิดขึ้น และมูลค่าเฉลี่ยของแต่ละออเดอร์

💡 เราจะใช้ Aggregate Functions เพื่อสรุปตัวเลขสำคัญ

### **1. ยอดขายรวม (Total Revenue) และ จำนวนออร์เดอร์ทั้งหมด (Total Orders)**
```sql
SELECT 
    SUM(total)                 AS total_revenue,
    COUNT(DISTINCT invoice_id) AS total_order
FROM supermarket_sales;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/total_rev.jpg)

🍁 คำนวณผลรวมของคอลัมน์ `‘total’` ซึ่งก็คือยอดขายรวมทั้งหมด และนับ `“invoice_id”` (รหัสบิล) ที่ไม่ซ้ำกัน เพื่อให้ได้จำนวนออเดอร์ทั้งหมด (1 บิล คือ 1 ออเดอร์)

### **2. ยอดขายรวม (Total Revenue) แบ่งตามประเภทสินค้า**
```sql
SELECT 
    product_line,
    SUM(total)    AS total_salse
FROM supermarket_sales
GROUP BY product_line
ORDER BY SUM(total) DESC;
```

![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/total_salse_producline.jpg)

🍁 รวมยอดขายทั้งหมด แบ่งตามประเภทสินค้า แล้วเรียงลำดับจากมากไปน้อย จากผลลัพธ์เราจะเห็นว่า สินค้าประเภท `‘Electronic accessories’` มียอดขายสูงที่สุด

### **3. มูลค่าเฉลี่ยต่อออเดอร์ (Average Order Value – AOV)**
```sql
SELECT 
	ROUND(SUM(total * 1.0) / COUNT(DISTINCT invoice_id),2) AS avg_order_value
FROM supermarket_sales;
```

![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/avg-per-order.jpg)

🍁 เพื่อทำความเข้าใจว่า โดยเฉลี่ยแล้ว ลูกค้าหนึ่งออเดอร์ใช้จ่ายเงินประมาณเท่าไหร่ คำนวณได้โดยการนำ `‘total_revenue (ยอดขายรวม)’` มาหารด้วย `‘total_orders` (จำนวนออร์เดอร์ทั้งหมด)’

🍁Tip: การนำ `‘SUM(total) คูณด้วย 1.0‘` เป็นเทคนิคเพื่อให้ผลลัพธ์ที่ได้จากการหารเป็นตัวเลขทศนิยม (ไม่ถูกปัดเศษแบบจำนวนเต็ม)

### **4. สาขาไหนทำยอดขายได้มากที่สุด 🎉**
```sql
SELECT 
    branch,
    SUM(total) AS total_sale
FROM supermarket_sales
GROUP BY branch
ORDER BY SUM(total) DESC;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/branch_total_sale.jpg)

🍁 หาผลรวมแล้วแบ่งกลุ่มตามสาขา เพื่อดูยอดขายของแต่ละสาขา แล้วเรียงยอดขายจากมากไปน้อย จากผลลัพธ์สาขาที่มียอดขายมากที่สุดคือ `‘สาขา C 🎉’`  จากข้อมูลเราอาจจะต้องจัดโปรโมชันหรือเปลี่ยนกลยุทธ์ใหม่เพื่อกระตุ้นยอดขายของ `‘สาขา A’` เพิ่มเติม

----
### ปัญหาที่ 2: แนวโน้มยอดขายเปลี่ยนแปลงไปตามเวลาอย่างไร? (รายวัน & รายชั่วโมง)
🌻 การรู้ว่าช่วงเวลาใดที่มียอดขายสูงสุด จะช่วยให้ธุรกิจวางแผนการจัดตารางพนักงาน จัดโปรโมชัน หรือจัดการสต็อกสินค้าได้ดีขึ้น

### **1. แนวโน้มยอดขายรายวัน (Daily Sales Trend)**
```sql
SELECT 
    date       AS sale_date,
    SUM(total) AS daily_total_sale
FROM supermarket_sales
GROUP BY date
ORDER BY date ;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/sale_date.jpg)

🍁 ดูว่ายอดขายรวมในแต่ละวันเป็นอย่างไร โดยใช้ `‘SUM(total)’` คำนวณผลรวมยอดขายสำหรับแต่ละวัน `‘GROUP BY date’` จัดกลุ่มยอดขายทั้งหมดที่เกิดขึ้นในวันเดียวกันเข้าด้วยกัน ก่อนที่จะรวมยอด เสร็จแล้วเรียงลำดับผลลัพธ์ตามวันที่ จากเก่าสุดไปใหม่สุด

### **2. แนวโน้มออร์เดอร์รายชั่วโมง (Hourly Order Trend)**
```sql
SELECT 
    time                       AS sale_hour, 
    COUNT(DISTINCT invoice_id) AS total_order_hourly
FROM supermarket_sales
GROUP BY sale_hour
ORDER BY sale_hour;
```

![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/hourly.jpg)
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/image-1.png)

🍁 ระบุชั่วโมงที่พีคที่สุดของวัน หรือช่วงที่มีจำนวนออเดอร์สูงที่สุด เพื่อเตรียมความพร้อมพนักงาน หรือเป็นข้อมูลที่ช่วยในการตัดสินใจเกี่ยวกับการตลาดหรือช่วงจัดโปรโมชัน

### **3. ยอดขายรวมแบ่งตามรายเดือน (Monthly Total Sales)**
```sql
SELECT
    STRFTIME('%Y-%m', date)  AS month , 
    SUM(total)               AS monthly_total_sales
FROM supermarket_sales
GROUP BY month;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/monthly_total_sales.jpg)

🍁 ดูยอดขายรวมแบ่งตามรายเดือน ว่าแต่ละเดือนมียอดเท่าไหร่ หรือเดือนไหนมียอดขายมากที่สุด จากตัวอย่างเป็นเพียงข้อมูลที่จำลองขึ้นมาเลยมีข้อมูลเพียงสองเดือน และเดือนที่มียอดขายมากที่สุดคือเดือน `‘Jan, 2023’`

----
### ปัญหาที่ 3: ลูกค้าของเราคือใคร ซื้ออะไร และจ่ายด้วยวิธีไหน? (ข้อมูลเชิงลึกเกี่ยวกับลูกค้าและสินค้า)
🌻 ธุรกิจจำเป็นต้องเข้าใจฐานลูกค้าและประสิทธิภาพของสินค้า เพื่อปรับแต่งกลยุทธ์การตลาดและจัดการสต็อกให้เหมาะสม
### **1. ประสิทธิภาพยอดขายตามประเภทสินค้า (Sales Performance by Product Category)**
```sql
WITH categorySales  AS ( -- step 1: หายอดขายของแต่ละประเภทสินค้า
    SELECT 
        product_line,
        SUM(total)  AS category_revenue
    FROM supermarket_sales
    GROUP BY product_line
),  grandTotal      AS ( -- step 2: หายอดขายรวมทั้งหมด
    SELECT 
        SUM(total)  AS grand_total
    FROM supermarket_sales
)
 
SELECT  
     t1.product_line,
     t1.category_revenue,
     ROUND((category_revenue / grand_total) * 100, 2) AS percentage_of_total_sales
FROM categorySales AS t1, grandTotal AS t2
ORDER BY percentage_of_total_sales DESC;
```

![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/percentage_of_total_sales.jpg)

🍁 ค้นหาว่าสินค้าประเภทไหนที่สร้างรายได้มากที่สุด และคิดเป็นกี่เปอร์เซ็นต์ของยอดขายทั้งหมด จากผลลัพธ์ประเภทสินค้าที่ทำยอดขายได้มากสุดคือ `‘Electronic accessories’` มีสัดส่วนเปอร์เซ็นต์มากที่สุดคือ `‘41.1%’`

🍁 เราใช้เทคนิคที่เรียกว่า `CTE (Common Table Expression)` เพื่อแบ่งการคำนวณออกเป็น 2 ส่วนย่อยๆ ก่อน
- categorySales คำนวณรายได้รวมของแต่ละ product_line (ประเภทสินค้า)
- grandTotal คำนวณรายได้รวมทั้งหมดของทุกสินค้า
- ในส่วน SELECT หลัก เรานำรายได้ของแต่ละประเภท (category_revenue) หารด้วยรายได้รวมทั้งหมด (grand_total) แล้วคูณ 100.0 เพื่อหาเปอร์เซ็นต์ จากนั้นปัดทศนิยมให้เหลือ 2 ตำแหน่ง และเรียงลำดับจากเปอร์เซ็นต์มากไปน้อย

### **2. ยอดขายตามประเภทลูกค้าและเพศ (Sales by Customer Type & Gender)**
```sql
SELECT 
    customer_type,
    gender,
    SUM(total)                  AS total_sales,
    COUNT(DISTINCT invoice_id)  AS total_orders
FROM supermarket_sales
GROUP BY customer_type, gender;
```

![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/customertype_genser.jpg)

🍁 ทำความเข้าใจพฤติกรรมการซื้อของลูกค้าแต่ละประเภท (สมาชิก/ทั่วไป) และลูกค้าแต่ละเพศ โดยจัดกลุ่มยอดขายและจำนวนออร์เดอร์ แบ่งย่อยตาม `customer_type` และ `gender` พร้อมกัน เพื่อดูว่ากลุ่มลูกค้ามีการซื้อขายอย่างไร

🍁 จากผลลัพธ์ กลุ่มลูกค้าที่มียอดซื้อและจำนวนออเดอร์มากที่สุดคือ`เพศหญิง (Female)` ที่เป็นลูกค้าประเภท`สมาชิก หรือ ‘Member’` นั่นเอง

### **3. วิธีชำระเงินที่ได้รับความนิยม (Popular Payment Methods)**
```sql
SELECT
    payment,
    COUNT(DISTINCT invoice_id)  AS n_transactions,
    SUM(total)                  AS total_revenue_by_payment
FROM supermarket_sales
GROUP BY payment
ORDER BY n_transactions DESC;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/payment_transactions.jpg)

🍁 ระบุวิธีชำระเงินที่ลูกค้าใช้บ่อยที่สุด โดยรวบรวมจำนวนธุรกรรมและรายได้ตามวิธีชำระเงิน เพื่อวิเคราะห์ว่าวิธีใดมีการใช้งานมากที่สุดและสร้างรายได้สูงสุด และวิธีชำระเงินที่ลูกค้าใช้บ่อยมากที่สุดคือ `‘Cash 💰’`

### **4. สาขาไหนได้ Rating หรือคะแนนเฉลี่ยความพึงพอใจของลูกค้ามากที่สุด**
```sql
SELECT  
    branch,
    ROUND(AVG(rating),2) AS avg_rating
FROM supermarket_sales
GROUP BY branch
ORDER BY avg_rating DESC;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/rating_branch.jpg)

🍁 สาขาไหนได้คะแนนความพึงพอใจของลูกค้ามากที่สุด โดยนำคะแนน rating ของแต่ละสาขามาหาค่าเฉลี่ย แล้วเรียงลำดับคะแนนจากมากสุดไปน้อยสุด จากผลลัพธ์สาขาที่ได้คะแนนความพึงพอใจของลูกค้ามากที่สุดคือ `‘สาขา B🎉’`

----
### ปัญหาที่ 4: การแปลงข้อมูลดิบเพื่อข้อมูลเชิงลึกที่ดีขึ้น
🌻 ข้อมูลดิบที่ได้มา บางครั้งก็ไม่ได้อยู่ในรูปแบบที่พร้อมใช้งานเสมอไป เราอาจต้องแปลงคอลัมน์ที่มีอยู่ หรือสร้างคอลัมน์ใหม่
### **1. การคำนวณกำไรขั้นต้น (Gross Income)**
```sql
SELECT
    invoice_id,
    total,
    cogs,
    ROUND((total - cogs),2) AS Gross_Income_Calculated -- คำนวณกำไรขั้นต้น
FROM supermarket_sales
LIMIT 10; -- แสดงผล 10 แถวแรก
```

![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/gross_income.jpg)

🍁 แม้ว่าในข้อมูลจำลองของเราจะมีคอลัมน์ gross_income อยู่แล้ว แต่การคำนวณ (total – cogs) นี้แสดงให้เห็นว่าเราสามารถสร้างคอลัมน์ใหม่ขึ้นมาได้ โดยการนำข้อมูลจากตารางเก่ามาคำนวณค่าขึ้นมาใหม่

```sql
SELECT
    invoice_id,
    total,
    ROUND(total * 0.07, 2)  AS vat
FROM supermarket_sales;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/vat.jpg)

🍁 สร้างคอลัมน์ `vat 7%` ขึ้นมาใหม่ โดยการนำ `total * 0.07`

### **2. การจัดกลุ่มลูกค้า (Customer Segmentation)**
```sql
SELECT 
    customer_type,
    CASE 
    	WHEN customer_type = 'Member' THEN 'ลูกค้าประจำ'
        ELSE 'ลูกค้าทั่วไป'
    END AS customer_segment
FROM supermarket_sales;
```
![Result](https://datateathyme.wordpress.com/wp-content/uploads/2025/07/segment_cust.jpg)

🍁 คำสั่ง **`CASE`** ช่วยให้เราสร้างเงื่อนไขเพื่อจัดหมวดหมู่ข้อมูลในคอลัมน์ `customer_type` ใหม่ได้ตามที่เราต้องการ เช่น ถ้าเป็น `‘Member’ ก็จัดเป็น ‘ลูกค้าประจำ’` เป็นต้น ทำให้การแบ่งกลุ่มลูกค้ามีความยืดหยุ่นมากขึ้น

----
## 📜สรุป
โปรเจกต์ SQL Supermarket Analytics แสดงให้เห็นอย่างชัดเจนว่าทักษะ SQL พื้นฐานสามารถเปลี่ยนข้อมูลดิบให้กลายเป็น ข้อมูลเชิงลึก (Insights) ได้ จากการวิเคราะห์ยอดขาย พฤติกรรมลูกค้า ไปจนถึงประสิทธิภาพการดำเนินงาน เราได้เรียนรู้ที่จะตอบคำถามทางธุรกิจสำคัญๆ เช่น สินค้าหมวดหมู่ใดทำเงินสูงสุด สาขาใดมียอดขายโดดเด่น ช่วงเวลาใดคือ Golden Hour ของธุรกิจ และลูกค้ากลุ่มใดที่มีอิทธิพลต่อรายได้มากที่สุด

## 🗒สิ่งที่ได้เรียนรู้
การทำ Case Study นี้ตอกย้ำว่า SQL คือเครื่องมือที่จำเป็น ที่ขาดไม่ได้สำหรับ Data Analyst
การใช้ Aggregate Functions, การจัดกลุ่มข้อมูล (GROUP BY), การเรียงลำดับ (ORDER BY) รวมถึงเทคนิคอย่าง CTE (Common Table Expressions) และคำสั่ง CASE
ช่วยให้เราสามารถดึงข้อมูลที่ซับซ้อนออกมาวิเคราะห์และนำเสนอได้อย่างมีประสิทธิภาพ ไม่ว่าจะเป็นการคำนวณ KPI สำคัญ การดูแนวโน้มตามช่วงเวลา หรือการจัดกลุ่มลูกค้าเพื่อกลยุทธ์ที่แม่นยำขึ้น

----
✨🍫 Explore more of my work on my portfolio website: [https://datateathyme.wordpress.com](https://datateathyme.wordpress.com/2025/07/22/sql-supermarket-analytics-case-study/)
