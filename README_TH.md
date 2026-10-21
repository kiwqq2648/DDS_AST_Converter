# DDS AST Converter (ต้นแบบ)

แอป Android นี้เลือกไฟล์ ZIP ผ่านตัวเลือกไฟล์ของ Android แล้วค้นหา/แตกไฟล์ `.dds` ออกมาในโฟลเดอร์ app-specific external storage

## ข้อจำกัด AST
ยังไม่มีการแปลง DDS เป็น AST เพราะยังไม่มีเอกสาร/ตัวอย่างที่ยืนยันรูปแบบ AST เป้าหมาย การเปลี่ยนนามสกุลไฟล์ไม่ใช่การแปลงรูปแบบ และไฟล์ที่แตกออกมาจะยังเป็น DDS

## สร้าง APK
โปรเจกต์นี้ตั้งใจให้สร้าง APK ผ่าน GitHub Actions เนื่องจากการติดตั้ง Android SDK/NDK และการ build Android โดยตรงใน Termux บน Android อาจมีข้อจำกัดตามสภาพแวดล้อม

1. สร้าง repository ใหม่บน GitHub
2. อัปโหลดไฟล์ทั้งหมดในโฟลเดอร์นี้ไปที่ repository (รวม `.github/workflows/build-apk.yml`)
3. เปิดแท็บ Actions แล้วรอ workflow `Build Android APK` ทำงานเสร็จ
4. เปิด run ล่าสุด แล้วดาวน์โหลด artifact `DDS-AST-Converter-debug`
5. แตก ZIP artifact แล้วติดตั้ง `app-debug.apk` บน Android โดยอนุญาตการติดตั้งจากแหล่งนี้เมื่อระบบถาม

## ตำแหน่งไฟล์ที่แตก
ไฟล์ถูกบันทึกในโฟลเดอร์เฉพาะของแอป `Android/data/com.example.ddsastconverter/files/DDS_AST_Converter/output` ซึ่งบางแอปจัดการไฟล์อาจมองไม่เห็นโดยตรง

## ความปลอดภัย
แอปใช้ชื่อไฟล์ปลายทางแทน path ภายใน ZIP เพื่อป้องกัน path traversal และเติมเลขต่อท้ายเมื่อมีชื่อซ้ำ
