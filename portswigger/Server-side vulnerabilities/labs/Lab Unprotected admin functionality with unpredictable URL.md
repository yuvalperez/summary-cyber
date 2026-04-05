למעבדה זו יש אדמין פנאל  לא מוגן. הוא ממוקם במיקום בלתי צפוי, אך המיקום נחשף איפשהו באפליקציה.

פתור את בעיית המעבדה על ידי גישה לפאנל הניהול, ושימוש בו כדי למחוק את המשתמש carlos.
פתרון:
הלכתי  לsource בinspect חיפשתי רזמים הרמז הכי קל הוא admin אז חיפשתי ומצאתי פונקציה 
```
var isAdmin = false;
if (isAdmin) {
   var topLinksTag = document.getElementsByClassName("top-links")[0];
   var adminPanelTag = document.createElement('a');
   adminPanelTag.setAttribute('href', '/admin-v2wudt');
   adminPanelTag.innerText = 'Admin panel';
   topLinksTag.append(adminPanelTag);
   var pTag = document.createElement('p');
   pTag.innerText = '|';
   topLinksTag.appendChild(pTag);
}
```
ומה אנחנו רואים פה /admin-v2wudt בעצם מצאנו את הכתובת שינסו להסתיר בפנינו 