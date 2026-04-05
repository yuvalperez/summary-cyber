This lab is vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists:

- [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

פתרון : 
נלך לlogin נשים סתם משתמש וסיסמה ונראה שהשרת נותן לנו username invalid ואז נגש לburp suit,
נדליק interpret  וניקח את הקשה  למטה נראה username=a&password=a  נשים את worldlist שקיבלנו בpayload ונלחץ קליק ימיני על השם משתמש ונעשה payload positions ונתחיל  בsniper attack ונחפש בשינוי של האורך בalterwind נראה שהאורך ישנה ל3354 ואז  נשים בפרמטר של המשתמש alterwind וסיסמה נקח מworldlist שיביאו לנו נחזור על אותו תהליך וב12345 נראה שנקבל אורך של 191 והופ נכנסנו למשתמש .
אבל בתכלס בעולם האמיתי שworldlist  היה הרבה יותר ארוך אנחנו ניקח את Invalid username ונשתמש בוא כפרמטר מתי לעצור את הברוט פורס ואותו דבר גם לסיסמה 