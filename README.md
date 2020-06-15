# BackupCode_Modify_Mconnect3.0.2_task_120620_rev150620
Modify Task Packdata_continue between Write SDcard  15/06/2020
Version นี้ ตรวจสอบการทำงาน packdata  ในขณะ ที่ Write SDcard จาก FRAM เนื่องจาก FRAM เต็ม 32KB แล้ว 
แต่ข้อมูลที่ Pack ยังไม่ได้เขียน ลง RAM ต่อ 

#### การทดสอบ คือทำงานได้ โดยไม่ Reset  
เมื่อ Run firmware  task_CheckWiFiMqtt  start ,task_Packdata_continue start 
แต่ มี flag ที่ write_addeeprom >= 32000  
xsdwrite = 1; เริ่มเขียน SDcard 
ทำให้ Task_Packdata_continue Start , Task__CheckWiFiMqtt Stop  เริ่ม packdata และ เก็บใน array const char* xdataContinue[23];
ทำงานจน จบการเขียน SDcard จน xsdwrite = 0;
Task_Packdata_continue Stop , Task__CheckWiFiMqtt Resume 

***ใน version ต่อไปกำลังทดสอบ Task Write Ram เมื่อ Clear Ram แล้ว หลังจาก Write SDcard เสร็จ 
หลัง การทำงานนี้ 
mac.writeAddress(writeaddr_eeprom1, 0); 
mac.writeAddress(writeaddr_eeprom2, 0);
write_addeeprom = 0;

