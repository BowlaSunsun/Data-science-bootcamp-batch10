## Homework5: Vlookup
### 🏷  โจทย์คือ ให้ดึงข้อมูลเกี่ยวกับ Position ด้านล่างขึ้นมาด้านบน 
**🖼 *'match position by vlookup'*** 
![Hw #2 _ Vlookup(Full)](https://github.com/user-attachments/assets/8ba6efea-1eda-470c-a261-2d8df4e370ff)

- **```=VLOOKUP(เลือกคอลัมน์ที่เราจะใช้ค้นหา, กำหนดช่วงของคอลัมน์ (ตารางที่เราจะค้นหา), ระบุว่าเราต้องการดึงข้อมูลจากคอลัมน์ที่ 2, 3, 4, 5, 6 (คอลัมน์ไหนบ้างที่เราสนใจ ทริคให้ใส่ {2,3,4,5,6} ), เลือกค่า FALSE เป็นแบบ 'exactmatch' เพื่อให้การค้นหาตรงกับข้อมูลที่เราต้องการเป๊ะๆ )```**
  
- ```javascript
     =ArrayFormula(VLOOKUP(H5:H29,A44:E47,{2,3,4,5},FALSE))
     -- ใช้ ArrayFormula เพื่อ copy สูตรอัตโนมัติในเซลล์เดียว เป็นการเขียนสูตรในเซลล์เดียว
     ช่วยประหยัดเวลาไม่ต้องคัดลอกสูตรลงไปทีละเซลล์  ทำงานกับข้อมูลจำนวนมากได้อย่างรวดเร็ว
     ```
![Hw #2 _ Vlookup](https://github.com/user-attachments/assets/3cfc3d2f-bcbf-475e-8fa5-63481a88de1c)



