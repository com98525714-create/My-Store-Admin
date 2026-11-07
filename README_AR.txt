لوحة صاحب المتجر - متجري
=========================

الملفات:
- owner.html / owner.css / owner.js: لوحة إدارة منفصلة للمالك.
- setup.sql: إنشاء جداول المنتجات والطلبات وسياسات RLS.
- نفس مشروع Supabase ونفس Publishable Key المستخدمين في تطبيق العملاء.

قبل التشغيل:
1) افتح Supabase > SQL Editor.
2) شغّل محتوى setup.sql مرة واحدة.
3) أنشئ حساباً من تطبيق العملاء، ثم أكّد البريد.
4) من Supabase > Authentication > Users انسخ UUID الخاص بحساب المالك.
5) في SQL Editor نفّذ:
   insert into public.store_owners(user_id) values ('UUID-HERE');
   واستبدل UUID-HERE بالمعرّف الحقيقي.
6) انشر مجلد لوحة المالك على استضافة HTTPS (مثلاً GitHub Pages أو Netlify)، ثم افتح owner.html.
7) سجّل الدخول بنفس حساب المالك الذي أضفته إلى store_owners.

الأمان:
- لا يوجد زر تسجيل مالك عام؛ صلاحية المالك تُمنح يدوياً من SQL Editor.
- جداول قاعدة البيانات محمية بسياسات Row Level Security.
- لا تضع أبداً service_role/secret key في ملفات HTML أو JavaScript.
- لا تشارك رابطاً عاماً للوحة المالك باعتباره حماية؛ الحماية الفعلية من قاعدة البيانات وRLS.

ملاحظة مهمة:
هذه اللوحة متصلة بجداول products وorders وorder_items التي ينشئها setup.sql.
نسخة متجر العملاء الحالية لا تزال تستخدم منتجات تجريبية، وواجهة الطلب فيها لا تحفظ الطلب بعد. لذلك لن تظهر طلبات العملاء هنا حتى نحدّث تطبيق العملاء في الخطوة التالية لقراءة المنتجات من جدول products وإرسال الطلبات إلى orders وorder_items.


إصلاح اتصال Supabase:
- تم تثبيت رابط المشروع الصحيح داخل owner.js:
  https://chlqszhbihtqlfghkxwn.supabase.co
- تم استخدام مفتاح Publishable الحالي.
- ارفع محتويات هذا المجلد كما هي، وتأكد أن index.html في جذر الموقع.
- لا تضع Service Role Key داخل ملفات الموقع.
