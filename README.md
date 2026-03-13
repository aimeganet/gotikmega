
📘 دليل مشروع Mega Net Flow - نظام إدارة مزودي خدمات الإنترنت (ISP Management Platform)
<div dir="rtl" align="right">
https://via.placeholder.com/800x200.png?text=Mega+Net+Flow+ISP+Platform

Mega Net Flow هو نظام متكامل لإدارة مزودي خدمات الإنترنت (ISP) مبني بأحدث التقنيات (Next.js 14، TypeScript، Tailwind CSS، Supabase). يوفر النظام واجهة حديثة لإدارة المشتركين، الباقات، الفواتير، مراقبة الشبكة، واكتشاف الأجهزة، مع دعم كامل للغة العربية والوضع الليلي (Dark Mode) ونظام صلاحيات متقدم.

</div>
📋 محتويات الدليل
المتطلبات الأساسية

التثبيت والإعداد

إعداد قاعدة البيانات (Supabase)

تشغيل المشروع محلياً

هيكل المشروع

الميزات الرئيسية

مهارات الذكاء الاصطناعي (AI Skills)

النشر على Vercel

استكشاف الأخطاء وحلولها

المساهمة والتطوير

🖥️ المتطلبات الأساسية
قبل البدء، تأكد من توفر ما يلي على جهازك:

Node.js الإصدار 18 أو أحدث

npm أو yarn أو pnpm

حساب في Supabase (مجاني)

حساب في GitHub (اختياري للنشر)

حساب في Vercel (اختياري للنشر)

نظام تشغيل: Windows 10/11، macOS، أو Linux

⚙️ التثبيت والإعداد
1. استنساخ المستودع
bash
git clone https://github.com/o08mega/mega-net-flow.git
cd mega-net-flow
2. تثبيت الاعتماديات
bash
npm install
أو باستخدام yarn:

bash
yarn install
3. إعداد متغيرات البيئة
أنشئ ملف .env.local في جذر المشروع:

env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
NEXT_PUBLIC_SUPABASE_URL و NEXT_PUBLIC_SUPABASE_ANON_KEY تجدها في Project Settings > API في لوحة تحكم Supabase.

SUPABASE_SERVICE_ROLE_KEY (سري) يُستخدم في Edge Functions ولا يُفضّل وضعه في الكود الأمامي.

🗄️ إعداد قاعدة البيانات (Supabase)
سجل دخول إلى Supabase وأنشئ مشروع جديد (اختر اسم مناسب ومنطقة قريبة).

بعد إنشاء المشروع، افتح SQL Editor والصق محتوى ملف database-schema.sql الموجود في مجلد ai-skills/DATABASE_SCHEMA (أو استخدم النص الكامل من هذا الرابط).

شغّل الأمر لإنشاء جميع الجداول والعلاقات وسياسات الأمان.

ملاحظة: هذا الأمر سينشئ كل الجداول المطلوبة: users، packages، subscribers، subscriptions، transactions، audit_logs، network_devices، network_links، device_logs، anomalies، ai_predictions، mikrotik_devices، import_logs.

بعد نجاح التنفيذ، انتقل إلى Authentication > Providers وفعّل مزود البريد الإلكتروني (Email) إن أردت تسجيل الدخول بالبريد وكلمة مرور.

🚀 تشغيل المشروع محلياً
بعد إعداد قاعدة البيانات ومتغيرات البيئة، شغّل المشروع:

bash
npm run dev
ثم افتح المتصفح على: http://localhost:3000

ستظهر الصفحة الرئيسية التي تعرض مهارات AI المحملة من مجلد ai-skills. هذا دليل على أن النظام يعمل.

📁 هيكل المشروع
text
mega-net-flow/
├── ai-skills/               # ملفات المهارات الذكية (النصوص التوجيهية)
│   ├── SKILL
│   ├── PROJECT_CONTEXT
│   ├── DATABASE_SCHEMA
│   ├── NETWORK_MODULE
│   └── DEBUG_PROTOCOL
├── src/
│   ├── ai/                  # كود تحميل المهارات
│   │   └── skill-loader.ts
│   ├── app/                  # تطبيق Next.js (App Router)
│   │   ├── (dashboard)/      # صفحات لوحة التحكم
│   │   ├── api/               # مسارات API
│   │   ├── auth/              # صفحات المصادقة
│   │   ├── layout.tsx
│   │   ├── page.tsx           # الصفحة الرئيسية (تعرض المهارات)
│   │   └── globals.css        # أنماط Tailwind
│   ├── components/            # مكونات React
│   ├── lib/                   # مكتبات مساعدة (Supabase, utils)
│   ├── hooks/                 # React Hooks مخصصة
│   ├── store/                 # حالة Zustand
│   └── types/                 # تعريفات TypeScript
├── supabase/
│   └── functions/             # Edge Functions
├── public/                    # ملفات ثابتة
├── middleware.ts              # حماية المسارات
├── next.config.js
├── tailwind.config.js
├── package.json
└── README.md                  # هذا الملف
✨ الميزات الرئيسية
لوحة تحكم احترافية - إحصائيات فورية، رسوم بيانية لحركة المرور، آخر المعاملات.

إدارة المشتركين - إضافة، تعديل، حذف، بحث متقدم.

إدارة الباقات - تحديد السرعة، السعر، الحصة.

الفواتير والمعاملات - تسديد المدفوعات، عرض السجل.

استيراد البيانات - رفع ملفات CSV/TXT مع معالجة النصوص العربية واكتشاف التكرارات.

مراقبة الشبكة - خريطة طوبولوجيا تفاعلية، اكتشاف أجهزة MikroTik، مقاييس حية، كشف الأنشطة المشبوهة.

تنبؤ بالإيرادات - باستخدام الذكاء الاصطناعي (نموذج متوسط متحرك).

نظام صلاحيات - ثلاثة أدوار: Super Admin، Admin، Member.

سجلات التدقيق - تتبع كل تغيير في النظام.

دعم كامل للغة العربية و RTL.

الوضع الليلي (Dark Mode) بنقرة زر.

مهارات AI - ملفات توجيهية تُقرأ وتُستخدم لتوسيع النظام.

🤖 مهارات الذكاء الاصطناعي (AI Skills)
المجلد ai-skills يحتوي على ملفات نصية تصف قدرات النظام وتوجه الذكاء الاصطناعي لبناء مكونات إضافية. يمكن استخدامها مع أدوات مثل Codex أو Copilot لتوليد كود جديد.

SKILL: وصف عام لمهارة AI.

PROJECT_CONTEXT: سياق المشروع الكامل.

DATABASE_SCHEMA: مخطط قاعدة البيانات (مكرر).

NETWORK_MODULE: وحدة اكتشاف الشبكة.

DEBUG_PROTOCOL: بروتوكول لتصحيح الأخطاء.

عند تشغيل المشروع، ستظهر هذه الملفات في الصفحة الرئيسية. يمكنك توسيع النظام بكتابة مهارات جديدة واستخدامها مع AI Agent.

🌐 النشر على Vercel
ادفع الكود إلى مستودع GitHub.

سجل دخول إلى Vercel وأنشئ مشروع جديد.

اختر المستودع.

أضف المتغيرات البيئية (نفس الموجودة في .env.local).

انقر Deploy.

بعد نجاح النشر، سيكون لديك رابط مباشر للتطبيق.

نشر Edge Functions
تحتاج أيضاً إلى نشر دوال Supabase Edge Functions:

bash
npm install -g supabase
supabase login
supabase link --project-ref your-project-ref
supabase functions deploy collect-device-metrics
supabase functions deploy predict-revenue
supabase functions deploy discover-mikrotik
supabase functions deploy analyze-anomalies
يمكن جدولة هذه الدوال باستخدام Supabase Cron (يتطلب خطة مدفوعة) أو باستخدام خدمة خارجية مثل cron-job.org.

❓ استكشاف الأخطاء وحلولها
المشكلة: خطأ relation "public.users" does not exist
الحل: تأكد من تنفيذ ملف SQL الكامل في Supabase. قد تحتاج لإعادة تشغيله.

المشكلة: البحث الذكي لا يعمل
الحل: تحقق من أن lodash.debounce مثبت بشكل صحيح، وأن دالة البحث في useSmartSearch تستخدم عمود name و phone و mac_address.

المشكلة: خريطة الشبكة لا تظهر
الحل: تأكد من تثبيت vis-network و vis-data. أيضاً تأكد من وجود بيانات في جداول network_devices و network_links.

المشكلة: Edge Function تفشل عند النشر
الحل: استخدم supabase functions deploy مع تحديد الإصدار. تأكد من أن الدالة لا تحتوي على أخطاء في الاستيراد (Deno).

🤝 المساهمة والتطوير
نرحب بمساهماتكم! يرجى اتباع الخطوات:

Fork المستودع.

أنشئ فرعاً جديداً (git checkout -b feature/awesome).

نفذ التغييرات وأضف اختبارات إن أمكن.

ادفع التغييرات (git push origin feature/awesome).

افتح Pull Request.

يرجى الالتزام بأسلوب الكود الموجود واستخدام TypeScript.

📄 الترخيص
هذا المشروع مرخص تحت رخصة MIT - انظر ملف LICENSE للتفاصيل.

📞 الدعم والاستفسارات
للاستفسارات والدعم، يرجى فتح issue في GitHub أو التواصل عبر البريد الإلكتروني: support@meganetflow.com (عنوان وهمي).

شكراً لاستخدامك Mega Net Flow! نتمنى لك تجربة ممتعة.

