This lab has a stock check feature which fetches data from an internal system.

To solve the lab, change the stock check URL to access the admin interface at `http://localhost/admin` and delete the user `carlos`.

פתרון: 
נלך לinspect נחפש http ונראה איזה בקשות הוא שולח, שנכנסים למוצר הוא מבקש מhttp כמה מוצרים יש בסטוק עם נשנה את זה ל`http://localhost/admin` נקבל admin panel אבל רגע אנחנו לא יכולים למחוק זה אומר לנו  שרק אמינים יכולים, 
למה ? כי אין לנו באמת את הגישה מי שכיביכול יש את הגישה זה השרת הפנימי.
נלחץ inspect על הdelte של carlos ונתקבל את הכתובת שמוחקת
`<a href="/admin/delete?username=carlos">Delete</a>  
עכשיו נוסיף `http://localhost/admin/delete?username=carlos">Delete` 
עכשיו נחזור ל`http://localhost/admin` ונראה שמחקנו.
