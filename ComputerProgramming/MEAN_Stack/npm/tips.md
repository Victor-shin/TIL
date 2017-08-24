### 메일 제목 인코딩 문제
  ```javascript
    subject = "=?utf-8?b?" + (new Buffer(subject)).toString('base64') + "?=";
    var mail = new Email({ 
        from: mailSender,
        to: job.mail,
        subject: subject,
        bodyType: "html",
        body: body,
    });
    mail.send();
```
