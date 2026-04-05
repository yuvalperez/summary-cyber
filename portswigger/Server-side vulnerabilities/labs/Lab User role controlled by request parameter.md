אני מדביק את מה שצריך לעשות (אני עצלן )
This lab has an admin panel at `/admin`, which identifies administrators using a forgeable cookie.

Solve the lab by accessing the admin panel and using it to delete the user `carlos`.

You can log in to your own account using the following credentials: `wiener:peter`
פתרון:
כבר אמרו לנו שזה cookie אז נחפש בinspect בapplication נלך לcookie נכנס למשתמש נעשה login ואז נראה admin = false ונשנה לTrue חשובבב עם T  גדולה ואז נלך ל`/admin` ונמחוק את carlos.

פתרון דרך burp suit:
1. Browse to `/admin` and observe that you can't access the admin panel.
2. Browse to the login page.
3. In Burp Proxy, turn interception on and enable response interception.
4. Complete and submit the login page, and forward the resulting request in Burp.
5. Observe that the response sets the cookie `Admin=false`. Change it to `Admin=true`.
6. Load the admin panel and delete `carlos`.
(העתקתי איו לי כוח לרשום אחרי שרשמתי כבר אבל חשוב לדעת את הדרך הזאת גם)
