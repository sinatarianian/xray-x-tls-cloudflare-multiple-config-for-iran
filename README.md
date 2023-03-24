# xray-(x)tls-cloudflare-cdn-multiple-config-for-iran
راهنمایی برای راه‌اندازی و تنظیم فیلترشکن v2ray xray برای ایران / مناسب سرور برای مصارف شخصی

 توجه: این راهنما مناسب کسانیست که کمی اطلاعات اولیه درباره‌ی مفاهیمی همچون سرور و کلادفلر دارند.

در ادامه تمام اقدامات لازم برای راه‌اندازی و تنظیم v2ray مبتنی بر xray-core رو منتشر میکنم. با تجربه‌ای که از ۵ ماه گذشته به دست آوردم این تنظیمات بهترین حالتیه که فعلا بعد از گذشته سه روز و با میانگین ترافیک خروجی ۴ گیگ در اوج ساعت مصرف با بیش از ۳۰۰ یوزر هنوز بسته نشده.

از مزایای این تنظیمات اینه که نیازی به پیدا کردن آی‌پی تمیز برای کلودفلر نداره، با یه اسکریپت ساده هم میشه ۶ کانفیگ متفاوت خودکار روی پورت ۴۴۳ و TLS ساخت. و همینطور خودکار یه camouflage website هم میسازه.


## قدم اول
### ساخت سرور با آی‌پی تمیز
یکی از مزایای هتسنر اینه که ۲۰ ترابایت ترافیک رایگان روی هر vpc میده که خیلی مقرون‌به‌صرفه است.
من سرور منطقه Falkenstein رو میگیرم با دو گیگ cpu و ram. لازم به ذکره که شانس پیدا کردن آی‌پی تمیز از سرورهای هلسینکی بیشتره.
بعدش از یه سرور ایرانی یا از یه سیستم با نت همراه‌اول یا ایرانسل یا ثابت یه ping میگیرم تا اول مطمئن بشم که صفر درصد packet loss داشته باشه.


## قدم دوم
### دامنه
پیشنهادم اینه که دامنه‌ی کشورهای اروپایی ccTLD خریداری بشه. مثلا آلمان. دلیلش هم اینه که به نظرم چون سفارت‌خانه‌ها باید با کشورهاشون در تماس باشند بلاک کردن دامنه‌های کشورها هزینه‌ داره برای همین بسته شدش خیلی دور از ذهنه.


## قدم سوم
### کلادفلر
دامنه رو در کلادفلر وارد کنید و پس از ست کردن NS در رجیسترار شروع کنید به تنظیم دقیقا به شکل زیر

#### DNS
حتما یه زیردامنه با IPv4 بسازید مثل مورد زیر.
فراموش نکنید که حتما در این مرحله پروکسی خاموش باشه.

<img width="1271" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222556546-14d53462-af8f-4d1a-b783-26dddc44ae2f.png">

این مورد رو باید برای رجیسترارتون بفرستید تا براتون ست کنه. البته جایی مثل goDaddy امکان ست کردن رو در پنل کاربر باز گذاشته.

<img width="1034" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222557159-5f4d2ecb-c3e1-48dd-a506-46647f613b83.png">

#### SSL/TLS
مد گواهی رو هم روی Full بذارید.

<img width="1038" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222557407-362ff8f2-fc33-462f-9449-5c00d93f6939.png">

این گزینه روشن باشه حتما

<img width="1034" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222558535-b264ff0b-9128-440c-ac85-9bb2bd8eb4a3.png">

این گزینه حتما روی TLS 1.3 باشه که میتونم بگم یکی از کلیدی‌ترین تنظیماتیه که باید رعایت بشه

<img width="1037" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222559477-050cc9ea-82ef-4dd3-a63f-17070e499332.png">

گزینه‌های زیر هم همگی روشن باشن

<img width="1037" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222559740-e3c0440a-51a7-4fc7-9016-b39993628106.png">

<img width="1040" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222560530-83a30252-99f1-4b10-ac5a-ebec1b114bfa.png">

#### Security
برای جلوگیری از سواستفاده از فیلترشکن از کشورهای دیگه حتما ترافیک ورودی به سمت سرور رو برای غیر از ایران ببندید.

<img width="1068" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222561693-cb3047c3-8cd6-40f4-ae03-263da3fda3aa.png">

حتما این مورد زیر رو هم Essenially off بذارید.

<img width="1042" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222562357-35598ffd-6632-4ec4-a100-ae00ccedec31.png">

موارد زیر هم من روشن گذاشتم

<img width="1041" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222562487-6c420f5d-98d0-4117-8646-da91137ebee0.png">

#### Network
گزینه‌های زیر روشن باشه.

<img width="1041" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222562740-769e6f1d-e66b-4e7e-a61b-a82a47bd6d97.png">

<img width="1037" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222562878-0838daec-896c-4ed1-8f4f-6bfa47f6df0d.png">

مورد زیر رو هم Add Header بذارید.

<img width="1034" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222563786-41a56558-8589-403b-a700-5e228375952e.png">

بقیه موارد رو هم تغییر ندادم و همون تنظیمات پیشنهادی خود کلادفلر گذاشتم.


## قدم چهارم

### نصب با اسکریپت mack-a
[لینک منبع اسکریپت](https://github.com/mack-a/v2ray-agent) ورژن انگلیسی هم داره این اسکریپت ولی من خودم اسکریپت چینی رو ران میکنم همیشه و با گوگل‌ترنسلیت ترجمه میکنم.

#### فایروال
پورت‌های ۲۲ و ۴۴۳ رو با ufw باز کنید.

#### اسکریپت
دستور زیر رو اجرا کنید:

run ```wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/master/install.sh" && chmod 700 /root/install.sh && /root/install.sh```

گزینه‌ی Xray-core رو انتخاب کنید.

از لیست حتما Install in any combination رو انتخاب کنید.
از مزایای این اسکریپت اینه که روی یک پورت میتونید هر ۶ ترنسپورت+پرتکل زیر رو انتخاب کنید
.
VLESS + TCP [TLS/XTLS]

VLESS + WS [TLS]

Trojan + gRPC [TLS]

VMess + WS [TLS]

Trojan + TCP [TLS]

VLESS + gRPC [TLS]

پورت رو هم حتما 443 انتخاب کنید.

حتما با letsencrypt یه گواهی SSL برای رمزگذاری ترافیک بسازید که با cloudflare وریفای بشه.

زمانی که به مرحله‌ای رسیدید که از شما درباره‌ cloudflare CNAME پرسید که میشه گزینه‌ 6/17 حتما گزینه‌ دو رو که دامنه who.int هست انتخاب کنید.

به کلادفلر برگردید و حالت پروکسی رو روشن کنید (به رنگ نارنجی) در بخش DNS

این امکان وجود داره که اولویت alpn رو به h2 تغییر بدید که برای اپ‌های آیفون که خیلی‌شون امکان ادیت کد رو نمیدن به‌کار میاد. برای این کار پس از اینکه تمام مراحل نصب به اتمام رسید، واژه ```vasma``` رو در ترمینال تایپ کنید و از منو شماره ۱۴ رو انتخاب کنید و طبق راهنما پیش برید.

برای اینکه مطمئن بشید دامنه شما تمیزه و در کل امکان اتصال بهش هست میتونید از این پکیج برای اوبونتو استفاده کنید.
[لینک](https://github.com/hatoo/oha/blob/master/README.md)


## قدم پنجم
### تنظیمات روی اپ
در انتهای اسکریپت به شکل خودکار براتون لینک‌های مجزا و لینک اشتراک به‌همراه QR code ساخته میشه.
دقت کنید که حتما uTLS روی Randomized باشه و alpn هم خالی نباشه و در صورت امکان روی h2 ست شده باشه.

نکته مهم: برای کانفیگ vless + tcp + xtls-vison حتما در بخش adress آی‌پی سرور رو قرار بدید. این کار رو برای Trojan + tcp هم انجام بدید تا متصل بشید.

نکته مهم دیگه: اگر احیانا کد بلاک شد حتما subdomain رو در قسمت SNI دستکاری کنید و به دلخواه تغییرش بدید. مثلا:

download.digitalrights.de -> iran.digitalrights.de
