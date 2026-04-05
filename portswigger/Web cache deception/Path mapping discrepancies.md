אי התאמות במיפוי נתיבים (Path mapping discrepancies) מפוי URL זה תהליך שיוך URL PATH למשאבים שעל השרת. יש כל מיני שיטות מיפוי מכל מיני frameworks (מסגרות).  שתי דרכים מוכרות  הן  traditional URL mapping ו RESTful URL mapping. 
מיפוי כתובות אתרים מסורתי( traditional URL mapping) מייצג נתיב ישיר למשאב הממוקם במערכת הקבצים. לעומת זאת, כתובות URL בסגנון REST אינן תואמות ישירות למבנה הקובץ הפיזי. הם מפשטים נתיבי קבצים לחלקים לוגיים של ה-API.
למשל פערים בין איך שהcache והשרת ממפים את המשאבים יכול לגרום ל web cache deception vulnerabilities . 
דוגמה אמיתית:
תוקף שולח: /user/123/profile/wcd.css

השרת (REST style): 
מתעלם מ wcd.css → מחזיר פרופיל של יוזר 123

ה cache (traditional):
רואה שה URL מסתיים ב .css → חושב שזה קובץ CSS
שומר את התגובה = פרטי הפרופיל של יוזר 123

עכשיו כל אחד שמבקש /user/123/profile/wcd.css
מקבל את הפרטים של יוזר 123 מה cache.

## Exploiting path mapping discrepancies: #Exploiting-path-mapping-discrepancies


**שלב 1 — בדיקת השרת:**

אתה שולח:

```
/api/orders/123/foo
```

`foo` זה מילה רנדומלית שהמצאת — לא קיימת באתר.

אם השרת עדיין מחזיר את פרטי ההזמנה = הוא מתעלם מ `foo` ורואה רק את `/api/orders/123`

זה אומר שהשרת גמיש עם ה URL — מה שאנחנו צריכים.


**שלב 2 — בדיקת ה cache:**

עכשיו מוסיפים סיומת סטטית:

```
/api/orders/123/foo.js
```

אם התגובה נשמרה ב cache = מצאנו פגיעות כי:

- השרת ראה `/api/orders/123` → החזיר מידע דינמי רגיש
- ה cache ראה `.js` → שמר את זה כאילו סטטי


**שלב 3 — למה מנסים סיומות שונות?**

כי לכל cache יש חוקים שונים — אחד שומר `.js` אחר שומר `.css` וכו.

צריך לנסות כמה עד שמוצאים איזו סיומת ה cache שומר.[

[Lab Exploiting path mapping for web cache deception]]
