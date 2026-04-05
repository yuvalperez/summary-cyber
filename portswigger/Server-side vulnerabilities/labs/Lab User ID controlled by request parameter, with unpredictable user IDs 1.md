This lab has a horizontal privilege escalation vulnerability on the user account page, but identifies users with GUIDs.

To solve the lab, find the GUID for `carlos`, then submit his API key as the solution.

You can log in to your own account using the following credentials: `wiener:peter`
פתרון:
נכנס למשתמש שתנו לנו, שנכנס נראה (my-account?id=2d72afcb-7e4c-411c-9c51-729f9523e349) שזה אומר שהם משתמשים בid שקשה לנחש אז לך לפוסטים של carlos או תגובות, אחרי חיפוש קצרצר מצאנו פוסט של הקורבן , נלחץ על פרופיל שלו ונראה (blogs?userId=0c1c57d4-00b9-4232-aa43-063ccf952a66) והינה מצאנו את ה id שלו עכשיו נשים את זה במקום שלנו בmy account  ונקח את הAPI key וסיימנו  