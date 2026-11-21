בתחילת השיעור בנינו את ה-images עם -t shoplist-backend:local. למה לא השתמשנו בשמות ש-Compose נתן (docker-backend)? ומה היה קורה בלי imagePullPolicy: Never?
פענחו את POSTGRES_PASSWORD מה-Secret. איזו פקודה הרצתן? מה זה אומר על האבטחה של Secret?
מחקתן את ה-pod של postgres והמוצרים נשארו. איזה קובץ אחראי לזה, ואיזו פקודה כן הייתה מוחקת אותם?
ב-Compose היה depends_on. ב-Kubernetes אין. מה קורה אם ה-backend עולה לפני postgres? מה דואג שהוא לא יקבל בקשות לפני שהוא מוכן?
ד8: מה ראיתן, ולמה? (ראו שם)
שיניתן ערך ב-app-config והרצתן apply, אבל ה-backend עדיין רואה את הערך הישן. למה, ומה הפתרון?
כמה פעמים כתבתן shoplist ב-12 הקבצים? ואם מחר נרצה להריץ עותק שני של ShopList ב-namespace בשם shoplist-test, כמה קבצים נצטרך לשנות? (רמז לשיעור הבא.)
