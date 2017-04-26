
# Mission 1: เริ่มต้น Bot ตัวแรกกับ Microsoft Bot Framework

ยินดีต้อนรับสู่ภารกิจที่ 1 ในภารกิจนี้พวกเราได้รับมอบหมายให้สร้างกลไกของ Bot และทดสอบมันให้แน่ใจว่ามันพร้อมขึ้นสู่วงโคจรในภารกิจถัดไป

สิ่งที่เราต้องมีบนเครื่องของเราในภารกิจนี้ คือ
- [Node.js](https://nodejs.org/en/) แบบ LTS เวอร์ชั่นล่าสุด ถ้าพวกเราเคยติดตั้ง Node.js มาก่อนแล้ว
สามารถรันคำสั่ง npm install npm -g เพื่ออัพเดตตัว Node.js ได้
- [Visual Studio Code](https://code.visualstudio.com/) (หรือ Editor อะไรก็ได้ที่เราถนัด)
- [Bot Framework Emulator](https://emulator.botframework.com/)

## 1. สร้างโฟลเดอร์เก็บโปรเจค Marsbot

ขั้นตอนแรกในภารกิจ เราจะทำการสร้างโฟลเดอร์ขึ้นมาชื่อ `Marsbot` และทำการเปิดโฟลเดอร์
ขึ้นมาในโปรแกรม Visual Studio Code

การเปิดโฟลเดอร์ขึ้นมาทำงานบนโปรแกรม Visual Studio Code สามารถทำได้ผ่านเมนู
**File > Open Folder** หรือการลากโฟลเดอร์มาวางบนหน้าต่าง Visual Studio Code

จากนั้นเราสามารถเปิดส่วนของ Integrated Terminal ได้ผ่านเมนู **View > Integrated Terminal**

เราจะสั่ง `npm init` และกรอกข้อมูลสำหรับ Bot ของเรา แน่นอนว่าบางส่วนสามารถใช้
ค่าเริ่มต้นแทนก็ได้ กรอกจนเสร็จจะมีข้อความยืนยันทั้งหมดอีกครั้ง ให้เรายืนยันโดยการพิมพ์ `yes` 

จากนั้นเราจะได้ไฟล์ `package.json` ในโฟลเดอร์ของเราประมาณนี้



ถ้าดูแบบผิวเผิน `package.json` จะทำหน้าที่เหมือนกับบัตรประชาชน ที่ระบุข้อมูลต่างๆ
เอาไว้ นี่เป็นหนึ่งในส่วนประกอบที่สำคัญของโปรเจค Bot เรา ซึ่งเราจะค่อยๆ เห็นหน้าที่ของมัน
ในภารกิจต่อๆ ไปครับ

## 2. ติดตั้ง Package ให้ Bot

ขั้นตอนต่อไปของภารกิจ เราจะติดตั้ง ส่วนประกอบเพิ่มดเติมให้ Bot ของเรา ด้วยการรันคำสั่ง 2
คำสั่งใน Terminal

```
npm install --save botbuilder
npm install --save restify
```

คำสั่งพวกนี้คือการติดตั้งสิ่งที่เสรียกว่า **Package** (หรือ dependencies) เพิ่มเติมเข้าไปในโปรเจค โดยนักพัฒนาสามารถสร้าง Package พวกนี้ไว้ใช้งาน หรือแจกจ่ายให้คนอื่นใช้งานได้ ซึ่ง package ที่เรานำมาใช้งานคือ **BotBuilder** ของ Microsoft และ **Restify** นั่นเอง

Microsoft BotBuilder เป็น Framework ที่เราจะใช้ในการจัดการกล่องโต้ตอบต่างๆ และ
เก็บข้อมูลของผู้ใช้ ส่วน Restify จะใช้ในการเชื่อมต่อ Bot ของเรากับ Web service อื่นๆ ผ่าน API

ในตอนนี้ถ้าเราเปิดไฟล์ `package.json` จะเห็นว่าในส่วนของ dependencies มีชื่อ
และเวอร์ชั่น Package ของ BotBuilder และ Restify อยู่ เกิดจากการสั่ง `--save` เพิ่มเติมในคำสั่งติดตั้ง Package เพื่อระบุว่าโปรเจคเรามีการอ้างใช้งาน package ทั้งสองตัวนั่นเอง

## 3. สร้างกลไกของ Bot ตัวแรก

เราจะสร้างไฟล์ index.js และคัดลอก code ด้านล่างนี้มาแปะไว้ในไฟล์

```

// Reference the packages we require so that we can use them in creating the bot
var restify = require('restify');
var builder = require('botbuilder');
// =========================================================
// Bot Setup
// =========================================================

// Setup Restify Server
// Listen for any activity on port 3978 of our local server
var server = restify.createServer();
server.listen(process.env.port || process.env.PORT || 3978, function () {
	console.log('%s listening to %s', server.name, server.url);
});
// Create chat bot
var connector = new builder.ChatConnector({
	appId: process.env.MICROSOFT_APP_ID,
	appPassword: process.env.MICROSOFT_APP_PASSWORD
});
var bot = new builder.UniversalBot(connector);

// If a Post request is made to /api/messages on port 3978 of our local server, then we pass it to the bot connector to handle
server.post('/api/messages', connector.listen());
// =========================================================
// Bots Dialogs 
// =========================================================
// This is called the root dialog. It is the first point of entry for any message the bot receives
bot.dialog('/', function (session) {
// Send 'hello world' to the user
session.send("Hello World");
});

```

การทำงานของ Bot ในตอนแรกนี้เรียบง่ายมาก เราสั่งให้ Bot ทำการตอบกลับทุกข้อความของ
เราด้วยคำทักทายดังกล่าวครับ

## 4. เริ่มการทำงานของ Bot

ขั้นตอนสุดท้ายในภารกิจนี้เราจะทำการทดสอบว่า Bot ที่เรามีนั้นทำงานได้ปกติ ผ่านการใช้งาน
Bot Framework Emulator 

กลับมาที่โปรแกรม Visual Studio Code และรันคำสั่งด้านล่างใน Terminal

```
node index.js
```

คำสั่งนี้เป็นการรันโค้ดในไฟล์ `index.js` ให้ทำงาน ซึ่งในตอนนี้ Bot ของเราควรจะเริ่มทำงานแล้ว เราจะเห็น console แจ้งสถานะการทำงานใน Integrated Terminal

จากนั้น ให้เปิดการทำงานของ Bot Framework Emulator ที่ซึ่งเราน่าจะเห็นกล่องข้อความในส่วนด้านบน ซึ่งค่าของ Emulator URL ควรจะเป็น **http://localhost:9000/** และ Bot URL ควรเป็น **http://localhost:3978/api/messages** และตอนนี้เราสามารถเว้น Microsoft App ID และ Microsoft App Password ว่างไว้ก่อนได้ครับ

ตอนที่เราเปิดการทำงานของ Bot Emulator อยู่นี้ ถ้าเราพิมพ์ข้อความ และกดส่งใน Emulator บอทก็เราก็น่าจะตอบกลับมาด้วย ข้อความทักทายที่เรากำหนดไว้

และถ้าเราสังเกตใน Terminal ก็น่าจะเห็นข้อมูลการทำงาน รวมถึง Error ที่อาจเกิดขึ้นได้
เช่นเดียวกัน จุดนี้ หากต้องการหยุดการทำงานของ Bot ให้ใช้ปุ่ม **Ctrl + C** ใน Terminal

**ยินดีด้วย จากจุดนี้พวกเราผ่านภารกิจที่ 1 แล้วครับ!** 

พร้อมแล้วเราไปแสตนด์บายที่[ภารกิจที่ 2](https://github.com/teerasej/mission-to-mar-thai/blob/master/mission-2.md) กันเลย

