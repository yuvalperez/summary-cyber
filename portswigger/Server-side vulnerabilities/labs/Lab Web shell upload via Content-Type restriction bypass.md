This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this.

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`
פתרון : 
בהתחלה אמרתי רגע איך עושים את זה ואז ראיתי מה סיכמנו שצריך לשנות את זה בburp suit אז העלתי את הקובץ כתמונה ואז הלכתי לburp suit תפסתי את הבקשה הלכתי לריפיטר לקחתי את הsession ואת הGET איפה שהתמונה וurl אז הגשתי את הבקשה אבל רגע אני לא רוצה שזה ירוץ כתמונה אני רוצה שזה היה php אז מה עשיתי שינתי לsd.php במקום sd.jpg ובום
```
GET /files/avatars/sd.php HTTP/2
Host: 0a46001f043f094e8044497000fa00c1.web-security-academy.net
Cookie: session=Y7dkEgdjem4NDcaxSyepSlnIjXn2gXKZ
```
