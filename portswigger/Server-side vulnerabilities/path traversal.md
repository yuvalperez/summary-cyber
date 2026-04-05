מה זה מעבר בין תיקיות (What is path traversal) מאפשר לתוקף לקרוא  קבצים רגישים.
המתקפה מתבססת על /../.. 
לדוגמה `<img src="/loadImage?filename=218.png">` האתר מעלה קובץ בצורה כזאת הURL לוקח פרמטר `filename`  ומחזיר את תוכן הנדרש. ומה שזה נותן לנו פה בעצם גישה לכול הקבצים במערכת עם אין הגנות.
**באינדוס ../ ו..\ שתיהם תקינים***
מעבדה [[Lab File path traversal, simple case]]

מפה זה ai סליחה אבל רצתי עם המעבדות
### קיפת הגנות נפוצות (Common Obstacles) #Path-Traversal-Bypass

מפתחים מנסים לחסום את `../`, והנה הדרכים לעקוף אותם:

1. **שימוש בנתיב מוחלט (Absolute Path):** לפעמים השרת חוסם רק את הרצף `../` אבל לא חוסם גישה ישירה לשורש המערכת.
- **הניצול:** במקום לטפס למעלה, פשוט נותנים את הנתיב המלא.

- **דוגמה:** `filename=/etc/passwd` `[[Lab File path traversal, traversal sequences blocked with absolute path bypass]]`

2. **רצפים מקוננים (Nested Traversal):** השרת מוגדר למחוק את המחרוזת `../` מהקלט, אבל הוא עושה את זה רק פעם אחת (לא רקורסיבי).

- **הניצול:** נשתמש ב-`....//`. השרת ימחק את ה-`../` שבאמצע, ומה שיישאר זה שוב `../` תקין.

- **דוגמה:** `filename=....//....//....//etc/passwd` `[[Lab File path traversal, traversal sequences stripped non-recursively]]`

3. **קידוד URL (URL Encoding):** לפעמים השרת מבצע ניקוי (Sanitization) על הטקסט הרגיל, אבל אז מפענח אותו שוב לפני השימוש.

 **הניצול:** נקודד את הנקודות או הסלאשים:

- `.` הופך ל-`%2e`, `/` הופך ל-`%2f`.

- **קידוד כפול (Double Encoding):** `%252e%252e%252f`. `[[Lab File path traversal, traversal sequences stripped with superfluous URL-decode]]`

4. **אימות תחילת נתיב (Validation of start of path):** השרת בודק שהקלט חייב להתחיל בתיקייה מסוימת (למשל `/var/www/images`).
- **הניצול:** פשוט נשאיר את ההתחלה הנדרשת ומיד אחריה נרד למטה.

- **דוגמה:** `filename=/var/www/images/../../../etc/passwd` `[[Lab File path traversal, validation of start of path]]`
 
5. **סיומת קובץ ו-Null Byte (Null Byte Bypass):** השרת דורש שהקובץ יסתיים ב-`.png`.

- **הניצול:** נשתמש בתו Null (מיוצג כ-`%00`). הוא אומר למערכת הקבצים "עצרי כאן" ומתעלם מכל מה שבא אחריו.

- **דוגמה:** `filename=../../../etc/passwd%00.png` _(הערה: זה עובד בעיקר בגרסאות שרת/שפה ישנות יותר)._ `[[Lab File path traversal, validation of file extension with null byte bypass]]`


### 🛡️ איך מונעים Path Traversal? #Prevention

1. **הדרך הכי טובה:** להימנע לחלוטין מהעברת קלט משתמש ישירות לפונקציות של מערכת הקבצים.

2. **שימוש ב-Whitelist:** לאפשר רק שמות קבצים ספציפיים או תווים אלפא-נומריים בלבד.

3. **Canonicalization:** אחרי חיבור הנתיב, להשתמש בפונקציה של השפה (כמו `getCanonicalPath` ב-Java) כדי לקבל את הנתיב הסופי והנקי, ולוודא שהוא עדיין מתחיל בתיקייה המורשית ולא "ברח" לשורש המערכת.