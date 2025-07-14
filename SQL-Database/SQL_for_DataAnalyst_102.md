# 📂 SQL for Data Analysts 102: A Chinook Database Case Study
### ⛱ This area showcases foundational SQL skills essential for data analysis, demonstrated through practical queries on the chinook.db database. 
**🌻filter data |**
```sql
SELECT * FROM customers
WHERE firstname = 'Leonie';
```
```sql
SELECT * FROM customers
WHERE country = 'USA'; -- key ที่ค้นหาต้องเหมือนในคอลัมน์เป๊ะๆ

-- ถ้าไม่แน่ใจว่าตัวอักษรในคอลัมน์นั้นเป็นตัวพิมพ์เล็กหรือพิมพ์ใหญ่ให้เปลี่ยนชื่อคอลัมน์เป็นตัวพิมพ์เล็กหรือพิมพ์ใหม่ทั้งหมดไปเลย
SELECT * FROM customers
WHERE LOWER(country) = 'usa'; -- เปลี่ยนตัวอักษรในคอลัมน์ให้เป็นตัวพิมพ์เล็กทั้งหมดเพื่อง่ายต่อการค้นหา
```
