This lab has a stock check feature which fetches data from an internal system.

To solve the lab, use the stock check functionality to scan the internal `192.168.0.X` range for an admin interface on port `8080`, then use it to delete the user `carlos`.

פתרון : אוקי אז  בעצם תרגיל קל אבל צורך לדעת להשתמש בburp suit אותו תהליך כמו מעבדה קודם רק דרך burp suit לוקחים את הבקשה של check stock עושים brute force בין `192.168.0.1`
ל`192.168.0.255` ואז רואים בstatus code  code 200 ורואים איזה ip זה ויש לנו את הip המתאים (אפשר לבדוק גם לפי האורך לא רק לפי הסטוטס קוד) 
http://192.168.0.162:8080/admin :התשובה 
http://192.168.0.162:8080/admin/delete?username=carlos
