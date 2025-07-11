# 📁 SQL & Excel Portfolio Project | Data Analyst Portfolio Project | For Beginners🌻
## 📑 PROBLEM STATEMENT
### 💡 KPIs REQUIREMENT
เราต้องการวิเคราะห์ key indicators หรือตัวชี้วัดสำคัญจากข้อมูลยอดขายพิซซ่า เพื่อให้เข้าใจประสิทธิภาพธุรกิจของเรามากขึ้น โดยเฉพาะอย่างยิ่ง เราจะคำนวณข้อมูลต่อไปนี้

1. Total Revenue (รายได้รวม ): ราคารวมของออร์เดอร์พิซซ่าทั้งหมด

2. Average Order Value (มูลค่าเฉลี่ยต่อออร์เดอร์): ยอดเงินเฉลี่ยที่ลูกค้าใช้จ่ายต่อ 1 ออร์เดอร์ (คำนวณจาก รายได้รวม หารด้วย จำนวนออร์เดอร์ทั้งหมด)

3. Total Pizzas Sold (จำนวนพิซซ่าที่ขายได้ทั้งหมด): ปริมาณพิซซ่าทั้งหมดที่ขายออกไป

4. Total Orders (จำนวนออร์เดอร์ทั้งหมด): จำนวนออร์เดอร์ที่ได้รับทั้งหมด

5. Average Pizzas Per Order (จำนวนพิซซ่าเฉลี่ยต่อออร์เดอร์): จำนวนพิซซ่าเฉลี่ยใน 1 ออร์เดอร์ (คำนวณจาก จำนวนพิซซ่าที่ขายได้ทั้งหมด หารด้วย จำนวนออร์เดอร์ทั้งหมด)

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
