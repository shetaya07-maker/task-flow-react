# TaskFlow | React Task Manager

مشروع React كامل مطابق لمتطلبات ملف Task Management System، مع فصل كل صفحة في ملف مستقل وتصميم قريب من المرجع: قائمة جانبية كحلي، خلفية فاتحة، وأزرار indigo. الواجهة باللغة الإنجليزية مثل التصميم المرفق.

## التشغيل على Visual Studio Code

1. ثبّت **Node.js 22 LTS أو إصدار LTS أحدث** مع npm. الحد الأدنى للمشروع Node.js 20.19.
2. فك ضغط الملف ZIP بالكامل، ثم افتح مجلد `taskflow-react` في Visual Studio Code عن طريق **File > Open Folder**.
3. افتح **Terminal > New Terminal**. تأكد أن التيرمنال داخل المجلد الذي يحتوي على `package.json`.
4. نفّذ:

```bash
npm install
npm run dev
```

5. افتح الرابط الذي يظهر في التيرمنال، وغالبًا سيكون `http://localhost:5173`.
6. لإيقاف التشغيل اضغط `Ctrl+C` في التيرمنال.

**لا تفتح `index.html` مباشرة ولا تستخدم إضافة Live Server لتشغيل React.** التشغيل يكون بالأوامر السابقة. أول تثبيت للحزم يحتاج إنترنت، ولا يتطلب المشروع حسابًا أو API key.

لو PowerShell على Windows منع `npm.ps1`، استخدم Terminal من نوع Command Prompt داخل VS Code، أو نفّذ `npm.cmd install` و`npm.cmd run dev` بدلًا من تغيير إعدادات أمان الجهاز.

## الصفحات

| الرابط | الصفحة | الملف |
| --- | --- | --- |
| `/` | Dashboard | `src/pages/Dashboard.jsx` |
| `/tasks` | My Tasks | `src/pages/Tasks.jsx` |
| `/add-task` | Add New Task | `src/pages/AddTask.jsx` |
| `/tasks/:id` | Task Details | `src/pages/TaskDetails.jsx` |
| أي رابط غير موجود | Not Found | `src/pages/NotFound.jsx` |

## المميزات

- إحصائيات إجمالي المهام والمكتمل والمعلق ونسبة الإنجاز، وتُحسب مباشرة من state.
- قائمة مهام تشمل العنوان والوصف والحالة وروابط التفاصيل.
- إضافة مهمة مع منع العنوان الفارغ أو المكوّن من مسافات فقط، ثم الانتقال إلى قائمة المهام.
- تبديل المهمة بين Completed وPending.
- حذف مهمة بعد رسالة تأكيد، مع إمكانية إلغاء الحذف.
- عرض بيانات المهمة المختارة، ورسالة مناسبة لو رقم المهمة غير موجود.
- البحث بالعنوان وفلترة المهام حسب الحالة.
- حالات فارغة للقائمة أو نتائج البحث، وتصميم متجاوب للموبايل والكمبيوتر.
- تسميات لعناصر الإدخال، دعم لوحة المفاتيح، ونافذة تأكيد قابلة للإغلاق بزر Escape.

## ملاحظات مهمة عن المتطلبات

- البيانات داخل `useState` فقط، كما يشترط الملف. **أي تحديث كامل للصفحة يعيد المهام الأربع الأصلية**. التنقل الداخلي بين الصفحات لا يفقد التغييرات.
- لا يوجد backend أو database أو localStorage أو Redux أو Zustand أو Context API.
- `BrowserRouter` و`Routes` و`Route` مستخدمة في Declarative Mode. لا يوجد `createBrowserRouter` أو `RouterProvider`.
- يوجد اختلاف داخل ملف المتطلبات بين شكل الصور وبيانات البداية المكتوبة: تم اتباع **بيانات البداية المكتوبة**. لذلك `Learn React` تبدأ Pending و`Learn useState` تبدأ Completed. الإحصائيات الأولية: 4 مهام، واحدة مكتملة، 3 معلقة، 25%.
- اسم Alex Morgan في الشريط الجانبي مجرد بيانات عرض مثل التصميم، وليس تسجيل دخول حقيقيًا. لا توجد خاصية حسابات مطلوبة.
- التنسيق في CSS عادي داخل `src/index.css`، وهو مسموح في ملف المتطلبات. لا توجد حاجة لتثبيت Tailwind.
- الميزات الإضافية المنفذة: البحث، فلترة الحالة، تأكيد الحذف. تعديل عنوان/وصف مهمة موجودة ليس ضمن المطلوب الإلزامي ولم تتم إضافته.

## تنظيم المشروع

```text
taskflow-react/
├── public/
│   └── favicon.svg
├── src/
│   ├── components/
│   │   ├── Navbar.jsx
│   │   ├── Sidebar.jsx
│   │   ├── Icon.jsx
│   │   ├── StatusBadge.jsx
│   │   ├── TaskCard.jsx
│   │   ├── TaskForm.jsx
│   │   ├── DeleteDialog.jsx
│   │   └── EmptyState.jsx
│   ├── data/
│   │   └── initialTasks.js
│   ├── pages/
│   │   ├── Dashboard.jsx
│   │   ├── Tasks.jsx
│   │   ├── AddTask.jsx
│   │   ├── TaskDetails.jsx
│   │   └── NotFound.jsx
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── tests/
│   └── taskflow.spec.js
├── index.html
├── package.json
├── package-lock.json
├── vite.config.js
├── playwright.config.js
├── TESTING.md
└── README.md
```

### مسار البيانات باختصار

`App.jsx` يحتفظ بالمهام ويحتوي على دوال الإضافة والحذف وتغيير الحالة. يرسل البيانات والدوال للمكونات عن طريق props. `TaskForm` يحتفظ بقيم الإدخال في `useState` ويستدعي دالة الإضافة، ثم يستخدم `useNavigate` للانتقال. صفحة التفاصيل تقرأ `id` من `useParams`. القوائم تُعرض باستخدام `map` مع `key` لكل مهمة.

## البناء والاختبار

```bash
npm run build
npm run preview
```

`build` ينشئ مجلد `dist`. أمر `preview` يشغّل نسخة البناء محليًا. التطبيق غير منشور على الإنترنت. لو قررت استضافته مستقبلًا، يحتاج السيرفر إلى SPA fallback إلى `index.html` حتى تعمل الروابط المباشرة لصفحات React Router.

لتشغيل اختبارات المتصفح الاختيارية بعد تثبيت الحزم:

```bash
npx playwright install chromium
npm test
```

الاختبارات تشغل خادم Vite تلقائيًا. تفاصيل الفحوص في `TESTING.md`. مجلد `node_modules` غير مرفق لتقليل حجم الملف؛ يتم إنشاؤه عند `npm install`. يُفضل الاحتفاظ بملف `package-lock.json`، ويمكن استخدام `npm ci` بدلًا من `npm install` لتثبيت الإصدارات المثبتة فيه.
