# יומן הרצה (Run Log)

## 1. בדיקת סביבה והתקנה ראשונית
- בוצעה בדיקת גרסת Node.js באמצעות `node --version`.
- בהרצת `npm install` הראשונה התקבלה שגיאת מערכת של npm:
  `npm error Exit handler never called! / This is an error with npm itself.`

## 2. טיפול בתקלות ופתרונות

### תקלה א': שגיאת Cache ופרוססים תקועים ב-npm
- **תופעה:** הרצת `npm install` נתקעה ולא יצרה את תיקיית `node_modules`.
- **פתרון:** 
  1. הרצת ניקוי מטמון: `npm cache clean --force` ו-`npm cache verify`.
  2. פתיחת הטרמינל כמנהל מערכת (Run as Administrator) וניקוי שאריות התקנה.

### תקלה ב': שגיאת תעודת אבטחה (SSL Certificate Chain)
- **תופעה:** התקבלה שגיאת רשת בעת הורדת החבילות:
  `npm error code SELF_SIGNED_CERT_IN_CHAIN` / `reason: self-signed certificate in certificate chain`
- **פתרון:** ביטול זמני של בדיקת ה-SSL המחמירה ב-npm באמצעות:
  `npm config set strict-ssl false`
  ולאחר מכן הרצת `npm install` מחדש והחזרת ההגדרה למצב תקין (`npm config set strict-ssl true`).

## 3. הרצת בדיקות ושרת (Status & Results)

- **התקנת חבילות:** הושלמה בהצלחה (נוספו 160 חבילות ונבנתה תיקיית `node_modules`).
- **בדיקת טיפוסים (Typecheck):** הפקודה `npm run typecheck` (`tsc --noEmit`) עברה בהצלחה ללא שגיאות.
- **הרצת בדיקות יחידה (Tests):** הפקודה `npm test` הרציאה את Vitest ועברה בהצלחה מלאה (5/5 בדיקות עברו - 100% Pass):
  - `requires a demo photographer identity`
  - `lists only events belonging to the requested photographer`
  - `does not return another photographer's event`
  - `allows a client to submit a selection for their own gallery`
  - `does not let a client access a different client's gallery`
- **הרצת שרת הפיתוח:** השרת הופעל בהצלחה בכתובת `http://localhost:3000` באמצעות `npm run dev`.
- **אימות מול השרת:** נבדק ה-endpoint לבדיקת תקינות (`http://localhost:3000/health`) והתקבלה תשובה תקינה: `{"status": "ok"}`.