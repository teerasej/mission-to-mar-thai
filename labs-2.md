# Lab 2: Facebook Bot

ประกาศ dialog เริ่มต้นด้านล่่างของ คำสั่ง `server.post('/api/messages', connector.listen());` โดยการแทนที่โค้ด Bot เดิม (สามารถ comment โค้ด Bot ตัวเดิมไว้) และทดสอบใน Bot Emulator และ Facebook Messenger

```
bot.dialog('/', function(session){
    session.endDialog('Hi, ' + session.message.user.name);
})
```

