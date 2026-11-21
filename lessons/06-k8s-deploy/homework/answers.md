בתחילת השיעור בנינו את ה-images עם -t shoplist-backend:local. למה לא השתמשנו בשמות ש-Compose נתן (docker-backend)? ומה היה קורה בלי imagePullPolicy: Never?
פענחו את POSTGRES_PASSWORD מה-Secret. איזו פקודה הרצתן? מה זה אומר על האבטחה של Secret?
מחקתן את ה-pod של postgres והמוצרים נשארו. איזה קובץ אחראי לזה, ואיזו פקודה כן הייתה מוחקת אותם?
ב-Compose היה depends_on. ב-Kubernetes אין. מה קורה אם ה-backend עולה לפני postgres? מה דואג שהוא לא יקבל בקשות לפני שהוא מוכן?
ד8: מה ראיתן, ולמה? (ראו שם)
שיניתן ערך ב-app-config והרצתן apply, אבל ה-backend עדיין רואה את הערך הישן. למה, ומה הפתרון?
כמה פעמים כתבתן shoplist ב-12 הקבצים? ואם מחר נרצה להריץ עותק שני של ShopList ב-namespace בשם shoplist-test, כמה קבצים נצטרך לשנות? (רמז לשיעור הבא.)


1 רצינו ש־Kubernetes ישתמש ב־Image המקומי שבנינו.כדי למנוע מ־Kubernetes לנסות להוריד את ה־Image מ־Registry, ולחייב אותו להשתמש ב־Image המקומי בלבד.
kubectl get secret postgres-secret -n shoplist -o jsonpath="{.data.POSTGRES_PASSWORD}" | base64 -d2t אינו מאובטח רק מעצם היותו Secret. ערכיו מקודדים ב־Base64 ולא מוצפנים כברירת מחדל, ולכן צריך להגן עליהם באמצעות הרשאות גישה מתאימות והצפנה של הנתונים במנוחה.
3postgres-pvc.yml
מחיקת ה־Pod לא מוחקת את הנתונים שבמסד הנתונים.
kubectl delete pvc postgres-pvc -n shoplist
הוא עלול לנסות להתחבר למסד הנתונים לפני שהוא מוכן, והחיבור ייכשל.משתמשים ב־Readiness Probe כדי לוודא שה־Backend מוכן לקבל בקשות, ורק אז ה־Service מנתב אליו תעבורה.
ConfigMap לא מעדכן אוטומטית משתני סביבה שכבר נטענו לתוך Pod קיים.
צריך לבצע Restart ל־Deployment כדי ליצור Pods חדשים שיטענו את הערכים המעודכנים.
מלא,
