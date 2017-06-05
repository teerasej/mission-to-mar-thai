# Mission 2: ส่ง Bot สู่ความเวิ้งว้างกับ Microsoft Azure 

จากภารกิจแรก เราได้ทำการสร้าง Bot และทดสอบใช้งาน แต่การที่จะให้มันเชื่อมต่อกับโลกภายนอก วิธีหนึ่งคือการติดตั้งมันลง Server และในที่นี้เราจะใช้ Microsoft Azure เป็นฐานให้กับ Bot ของเรา

สิ่งที่คุณต้องมีในภารกิจนี้ 

1. โปรเจค Bot จากภารกิจที่ 1 
2. Github Account [สมัครที่นี่](https://github.com/join?source=header-home) 
3. ติดตั้ง Git Client มีให้เลือกระหว่างใช้งานผ่าน [Git Command Line](https://git-scm.com/downloads) และเป็น Application ([Github Desktop](https://desktop.github.com/)) **อย่าลืมเลือกตัวเลือกติดตั้งลง Path ของระบบด้วย เพื่อให้เรียกใช้ได้ง่าย**
4. [ลงทะเบียน Visual Studio Dev Essential](https://www.visualstudio.com/dev-essentials/) เพื่อได้เครดิตใช้งาน Azure ฟรี เดือนละ 25 เหรียญ

## 1. ตั้งค่า package.json สำหรับ Web Service

เปิดไฟล์ `package.json` และกำหนดค่าตามนี้ 

```
{
...
    "main" : "index.js" ,
    "scripts" : {
        ...
        "start" : "node index.js"
    }
...
}
```

โดยไฟล์ `index.js` คือไฟล์โค้ดที่เราเขียน Bot เอาไว้ และคำสั่ง `start` ไว้สำหรับให้ Web Service เรียกใช้งาน สำหรับบางคนตั้งชื่อไฟล์เป็น `app.js` ก็ตั้งตามไฟล์ที่มีนะครับเช่น

```
{
...
    "main" : "app.js" ,
    "scripts" : {
        ...
        "start" : "node app.js" // 
    }
...
}
```

## 2. สร้าง Github Repository และเชื่อมกับโปรเจคในเครื่อง

เริ่มแรกเราจะทำการสร้าง Git Repository เพื่อเก็บไฟล์โปรเจค Bot ของเรา และใช้ในการเชื่อมต่อติดตั้งบน Microsoft Azure 

เริ่มจาก Sign in เข้าใช้ Github จากนั้นให้กดปุ่ม **+** ด้านบนขวา เลือกคำสั่ง New Repository

กรอกชื่อ Repository และ Description ตามต้องการ เว้นในส่วน `.gitignore` และ license ไว้ และกดปุ่ม **Create Repository**

เราจะได้ Repository เปล่าๆ มา 1 อัน จะเห็นว่า**เราได้ URL ของ Repository มา** ซึ่งเราจะใช้ในขั้นตอนต่อไป

## 3. ตั้งค่า Git ให้โปรเจค

กลับมาที่โปรเจคของเราใน Visual Studio Code ในส่วนของ Integrated Terminal ให้เรารันคำสั่ง

```
git init
```

และตามด้วย 

```
git remote add origin <Repository Url>
```

โดย Repository Url คือ Url ที่เราคัดลอกมาจากการสร้าง Repo ของเราในขั้นตอนที่แล้ว เช่น `https://github.com/teerasej/marsbot`

หลังจากรันแล้ว ในส่วนของ Git ใน Visual Studio Code จะเห็นว่ามีไฟล์มากมายรอให้ทำการ commit ขึ้น Repo ซึ่งบางส่วนก็ไม่จำเป็น เราสามารถกำหนดได้ว่าจะไม่ให้ git ทำการอัพโหลดโฟลเดอร์ไหนขึ้น Repo ด้วยไฟล์ **.gitignore**

## 4. สร้างไฟล์ .gitignore

ให้เราใช้คำสั่ง **File > New File** จากนั้นกรอกข้อความลงในไฟล์ดังนี้

```
node_modules/
```

จากนั้นให้บันทึกไฟล์ ตั้งชื่อไฟล์ว่า `.gitignore` (สังเกตว่ามี เครื่องหมาย “จุด” นำหน้าชื่อ) จะทำให้ git ไม่สนใจไฟล์ในโฟลเดอร์ `node_modules` ทั้งหมด

## 5. Commit ไฟล์ขึ้น Repo

กลับมาที่ Git ใน Visual Studio Code กรอกข้อความ ‘Initial Commit’ คงในช่อง message และกดปุ่ม Commit (เครื่องหมายถูก)

จากนั้นกดปุ่ม Option (เครื่องหมาย **...** ) เลือกคำสั่ง Publish และเลือก Origin เพื่อส่งไฟล์ในโปรเจคขึ้น Github Repository

## 6. สร้าง Azure App Service และ Deploy โปรเจคจาก Github 

ทำการสร้าง App Service บน Microsoft Azure และกำหนด Deploy โปรเจคจาก Github [ตามขั้นตอนใน Link นี้](http://nextflow.in.th/2017/how-to-deploy-chat-bot-to-microsoft-azure/)




