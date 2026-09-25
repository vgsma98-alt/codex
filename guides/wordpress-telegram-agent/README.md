# وكيل WordPress عبر Telegram — دليل المستخدم والوكيل

[تنزيل المشروع](../../wordpress-telegram-agent-source.zip)

الوكيل يستقبل طلبات التعديل عبر Telegram، يعرض اقتراحاً للتأكيد، ثم يرسل التعديل إلى WordPress. تتضمن الحزمة خادم Node.js في `server/` وإضافة WordPress في `ai-site-agent/` وملفات Docker وEasyPanel. اقرأ `README.md` داخل الحزمة للتثبيت الكامل. لا تتضمن الحزمة رموز البوت أو الإعدادات الحية.

## التثبيت

1. أنشئ بوتاً عبر BotFather، وجهّز خادماً بنطاق HTTPS وموقع WordPress.
2. انسخ `.env.example` إلى `.env` محلي أو أدخل قيمه في **Environment** في EasyPanel. أنشئ قيمتي `TELEGRAM_WEBHOOK_SECRET` و`ADMIN_API_KEY` مستقلتين؛ لا تأتيان من BotFather.
3. اضغط مجلد `ai-site-agent/` وحده إلى ZIP، ارفعه في **إضافات WordPress** ثم فعّله واستخرج سر الربط.
4. انشر `server/` باستخدام `compose.yaml` أو إعدادات `deploy/`، واختبر `/health`. اربط رقم محادثة العميل بالموقع، وسجّل Webhook، ثم جرّب طلباً وتأكيده.

## للمطور أو نموذج الذكاء الاصطناعي

فك الحزمة وافتحها في Codex. مسار Telegram في `server/src/telegram.js`، وتحليل الطلبات في `server/src/ai.js`، واتصال WordPress في `server/src/wordpress.js`، وتخزين الربط في `server/src/store.js`. شغّل `cd server` ثم `npm test` بعد تغيير الخادم. افحص PHP بواسطة `php -l ai-site-agent/ai-site-agent.php` إن توفر. تعديل الشيفرة لا ينشرها تلقائياً؛ حدث الخدمة بعد الاختبار.

لا تحذف ملفات قائمة دون موافقة المالك. احتفظ بالمفاتيح والرموز في متغيرات البيئة فقط، ولا ترفع `.env` أو بيانات العملاء إلى GitHub. الحزمة شيفرة مصدر وليست نسخة من محتوى WordPress الحي أو مخزن الوكيل المستمر؛ خذ نسخة احتياطية قبل تعديل الإنتاج.
