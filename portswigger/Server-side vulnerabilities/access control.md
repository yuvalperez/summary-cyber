אז מה זה בקרת גישה (access control)
בקרת גישה זאת מערכת  ששולטת על מיט מורשה לבצע בפעולה או לגשת למשאבים. 
היא תלויה על אימות ו sessions.
אימות: בודק שהיוזר הוא היוזר הנכון ולא מי שהוא  אומר שהוא.
סשן : מזהה אילו בקשות HTTP עוקבות מתבצעות על ידי אותו יוזר.
בקרת גישה : מחליט עם היוזר מורשה לבצע את מה שמנסה לבצע .
תכנון וניהול של בקרות גישה הוא בעיה מורכבת ודינמית להכן פריצות הן שכיחות התכנון צריך להתקבל  על ידי בני אדם ולכן יש פואנציאל לטעויות  .

Vertical privilege escalation: #vertical-privilege-escalation
הסלמה אנכית של הרשאות (Vertical privilege escalation ) מה זה בעצם אם המשתמש יכול לקבל גישה שהוא אינו מורשה לגשת אליה.
לדוגמה: משתמש רגיל שלא אדמין מקבל ארשות של אדמין.


Unprotected functionality: #Unprotected-functionality
פונקציות לא מוגנות (Unprotected functionality) הסלמה אנכית  (Vertical privilege escalation) בסיסית אשר היישום לא אוכף שום הגנה על פונקציה רגישהת  פונקציות אדמין  עשויות להיות נגישות דרך URL יוזר יוכל לגשת ל /administrator-panel מבלי להיות אדמין 
לרוב נמצא את הפונקציות בעזרת brute force או בעזרת java files שחוספים את הURL או בדרך הקוד של האתר .
לדוגמה : בדרך כלל `robots.txt` הוא קובץ טקסט סטטי בשרת דרך כלל נמצא נתיבים שהמתכנת החביא כדי לבנות את הממשק,
בתוך הURL שם אנחנו נמצא /administrator-panel  נכנס ל website.com/admin ואז השגנו שאדמין .

[[Lab Unprotected admin functionality]]
חידוד: במקרים מסיוימים פונקציות לא מוגנות היו בשם שקשה לנחש זה נקראה (security by obscurity) שזאת דרך לא יעילה להגן על הפונקציה בגלל שכנראה האתר יחשוף אותה בכמה דרכים ,
אחת מהן  כתובת ה-URL עשויה להיחשף ב-JavaScript שבונה את הממשק 
דוגמה : 
[[Lab Unprotected admin functionality with unpredictable URL]]



Parameter-based access control methods: #Parameter-based-access-control-methods
שיטות בקרת גישה מבוססות פרמטרים (Parameter-based access control methods:) מה זה בעצם 
יש אפליקציות  שמחליטה הרשאות של יוזר לפי פרמטר ושניתן ונגיש לישנוי על ידי המשתמש ,
יכול להיות שדה נסתר, cookie,פרמטר string שהוגדרה מראש
לדוגמה:
בcookie  יכול להיות admin=true  או role=1 וכדומה הדרך הזאת מסוכנת בגלל שכול יוזר יכול פשוט לגשת ולשנות לעצמו הרשאות.
[[Lab User role controlled by request parameter]]

Horizontal privilege escalation: #Horizontal-privilege-escalation
הסלמה אופקית של הרשאות (Horizontal privilege escalation)  בשונה להסלמה אנכית של הרשאות היוזר פה משיג גישה של יוזר אחר. 
אם למשל עובד בחברה  יכול להשיג גישה לעובד אחר בחברה זה סלמה אופקית התקפות דומות להתקפות  להסלמה אנכית למשל /myaccount?id=123 פה היוזר מואחסן על ידי id  ועם התוקף ישנה לid אחר הוא יקבל גישה של היוזר שהוא שם את הid שלו בלי שהאפלקציה תבדוק אם זה היוזר הנכון.
יש אפלקציות שיוזר לא היה בid פשוט אלה בGUIDs בשביל להיות פחות צפוי לתוקף אבל יכול להיות שיחשפו את הguid בפוסט,תגובה, עמוד פרופיל  וכו .

 [[Lab User ID controlled by request parameter, with unpredictable user IDs]]
 
Horizontal to vertical privilege escalation: #Horizontal-to-vertical-privilege-escalation
לעיתים קרובות נוכל להשיג מהסלמה אופקית(Horizontal) להסלמה אנכית(vertical)  בכך התקוף יתקוף משתמש של אדמין.
למשל התוקף ישיג id של אדמין במקום יוזר רגיל.
[[Lab User ID controlled by request parameter with password disclosure]]

מפה זה ai בגלל שרצתי עם מעבדות אבל סטייל של איך אני מסכם
### Insecure Direct Object References (IDOR): #IDOR

מה זה בעצם? מקרה פרטי של בקרת גישה לקויה שבו האפליקציה משתמשת בפרמטרים כדי לגשת ישירות לאובייקטים (קבצים, שורות במסד נתונים) בלי לבדוק הרשאות.

- **דוגמה:** אתר שמאפשר להוריד קבלות לפי שם קובץ: `static/download/receipt_101.pdf`.

- **הניצול:** התוקף פשוט משנה את המספר ל-`receipt_102.pdf` וצופה בקבלה של מישהו אחר.

- **חידוד:** זה יכול להיות ב-URL, בפרמטרים של POST או אפילו בתוך קבצי JSON שנשלחים לשרת. `Lab Insecure direct object references`




### Multi-step processes with no access control: #Multi-step-processes

מתקפה על תהליכים מורכבים. הרבה פעמים פונקציות (כמו שינוי הרשאות של משתמש) קורות בכמה שלבים:

1. בחירת משתמש.

2. בחירת התפקיד החדש.
   
3. **אישור סופי (Confirm).**


**הפרצה:** השרת בודק שאתה אדמין בשלב 1 ו-2, אבל בשלב 3 (הבקשה הסופית) הוא מניח ש"אם הגעת לפה, בטח עברת את הבדיקות הקודמות" ולא בודק שוב.

- **הניצול:** תוקף יכול לשלוח ישירות את בקשת ה-HTTP של השלב האחרון (למשל `action=upgrade&confirm=true`) ולדלג על כל שלבי הבדיקה. `Lab Multi-step process with no access control on one step`




### Platform-based access control bypass: #Platform-misconfiguration

לפעמים בקרת הגישה לא נמצאת בתוך הקוד של האתר, אלא בשרת (כמו WAF או Reverse Proxy). אפשר לעקוף אותה בכמה דרכים:

1. **שימוש ב-Headers של URL Override:** חלק מהמערכות מאפשרות להשתמש ב-Headers מיוחדים כדי "לעבוד" על השרת:
  - `X-Original-URL: /admin/deleteUser`

  - `X-Rewrite-URL: /admin/deleteUser` התוקף שולח בקשה לדף הבית `/` (שמותר לכולם), אבל ה-Header גורם לשרת הפנימי להריץ את הפקודה של האדמין. `Lab URL-based access control can be circumvented`

2. **עקיפה בעזרת שיטת ה-HTTP (Method Bypass):** השרת מוגדר לחסום בקשות `POST` ל-`/admin`.

- **הניצול:** נסה לשלוח את הבקשה כ-`GET`. אם הקוד בשרת לא בודק את סוג המתודה, הפעולה תתבצע למרות החסימה. `Lab Method-based access control can be circumvented`
 



### Referrer-based access control: #Referer-bypass

יש אתרים שבודקים אם אתה מורשה לגשת לדף מסוים לפי ה-Header שנקרא `Referer` (הדף הקודם שהיית בו).

- **הלוגיקה הפגומה:** "אם הוא הגיע מהדף `/admin`, סימן שהוא אדמין".

- **הניצול:** אנחנו שולטים ב-Headers ב-100% דרך Burp. פשוט נוסיף `Referer: https://website.com/admin` לכל בקשה ונעקוף את ההגנה. `Lab Referer-based access control`
  


### Location-based access control: #Location-bypass

בקרת גישה לפי המיקום הגיאוגרפי של המשתמש (לפי IP או GPS).

- **איך עוקפים?**

    1. **VPN/Proxy:** כדי לקבל IP של המדינה המותרת.
        
1. **זיוף Headers:** שימוש ב-Headers כמו `X-Forwarded-For` כדי לגרום לשרת לחשוב שה-IP המקורי שלנו שונה.

2. **זיוף GPS:** דרך ה-Console של הדפדפן (Sensors) כדי לשנות את הקואורדינטות שהדפדפן מדווח.


### איך מונעים פגיעות בבקרת גישה? (Defense) #Prevention

1. **Deny by default:** כל משאב חסום לכולם, אלא אם הוגדר במפורש שהוא ציבורי.
    
2. **לא לסמוך על הלקוח:** לעולם לא להסתמך על Headers כמו `Referer` או פרמטרים כמו `admin=true`.
3. **מנגנון מרכזי אחד:** אל תכתוב בדיקת הרשאות בכל דף בנפרד. תבנה פונקציה אחת שבודקת הכל ותריץ אותה בכל בקשה.
4. **בדיקה בכל שלב:** במידה ויש תהליך של כמה שלבים, לבדוק הרשאות בכל אחד מהשלבים מחדש.
