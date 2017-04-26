# Lab 1: Marsbot

คัดลอกโค้ดนี่ไปใส่ ด้านล่างคำสั่ง `server.post('/api/messages', connector.listen());` แทนที่โค้ดของ Bot เดิม (สามารถ comment โค้ด Bot ตัวเดิมไว้)

```

var intentDialog = new builder.IntentDialog();

bot.dialog('/', intentDialog);

intentDialog.onDefault(builder.DialogAction.send('Sorry, I didn\'t understand that.'));

intentDialog.matches(/^Greeting/i,'/greetingDialog');
intentDialog.matches(/^Size/i, '/sizeDialog');
intentDialog.matches(/^Distance/i, '/distanceDialog');
intentDialog.matches(/^Life/i, '/lifeDialog');

bot.dialog('/greetingDialog', 
    function(session)
    {
        session.endDialog('Hi! I\'m a droid from Mars. Ask me questions you have about Mars!');
    }
)

bot.dialog('/sizeDialog',
    function(session)
    {
        session.endDialog('Mars has a radius of 3,390km, compared to Earth\'s radius which is 6,371km');
    }
)

bot.dialog('/distanceDialog',
    function(session)
    {
        session.endDialog('Mars is pretty far away from your home planet, Earth. On average, the distance is 225 million km.');
    }
)

bot.dialog('/lifeDialog', 
    function(session)
    {
        session.endDialog('Yes, there is life on Mars although not yet discovered by primitive humans.');
    }
)
```