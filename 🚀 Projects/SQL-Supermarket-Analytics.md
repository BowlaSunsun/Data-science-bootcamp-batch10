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
