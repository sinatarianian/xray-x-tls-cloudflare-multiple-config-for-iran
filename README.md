# xray-tls-cloudflare-multiple-config-for-iran
راهنمایی برای راه‌اندازی و تنظیم فیلترشکن برای ایران

در ادامه تمام اقدامات لازم برای راه‌اندازی و تنظیم v2ray مبتنی بر xray-core رو منتشر میکنم. با تجربه‌ای که از ۵ ماه گذشته به دست آوردم این تنظیمات بهترین حالتیه که فعلا بعد از گذشته سه روز و با میانگین ترافیک خروجی ۴ گیگ در ساعت هنوز بسته نشده. از مزایای این تنظیمات اینه که نیازی به پیدا کردن آی‌پی تمیز برای کلودفلر نداره و با یه اسکریپت ساده هم میشه ۶ کانفیگ متفاوت خودکار ساخت.

## قدم اول
### ساخت سرور با آی‌پی تمیز
یکی از مزایای هتسنر اینه که ۲۰ گیگ ترافیک رایگان روی هر vpc میده که خیلی مقرون‌به‌صرفه است.
من سرور منطقه Falkenstein رو میگیرم با دو گیگ cpu و ram.
بعدش از یه سرور ایرانی یا از یه سیستم با نت همراه‌اول یا ایرانسل یا ثابت یه ping میگیرم تا اول مطمئن بشم که صفر درصد packet loss داشته باشه.

## قدم دوم
### دامنه
پیشنهادم اینه که دامنه‌ی کشورهای اروپایی ccTLD خریداری بشه. مثلا آلمان. دلیلش هم اینه که به نظرم چون سفارت‌خانه‌ها باید با کشورهاشون در تماس باشند بلاک کردن دامنه‌های کشورها هزینه‌ داره برای همین بسته شدش خیلی دور از ذهنه.

## قدم سوم
### کلادفلر
دامنه رو در کلادفلر وارد کنید و پس از ست کردن NS در رجیسترار شروع کنید به تنظیم دقیقا به شکل زیر

#### DNS
حتما یه زیردامنه با IPv4 بسازید مثل مورد زیر.

<img width="1271" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222556546-14d53462-af8f-4d1a-b783-26dddc44ae2f.png">

این مورد رو باید برای رجیسترارتون بفرستید تا براتون ست کنه. البته جایی مثل goDaddy امکان ست کردن رو در پنل کاربر باز گذاشته.

<img width="1034" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222557159-5f4d2ecb-c3e1-48dd-a506-46647f613b83.png">

#### SSL/TLS
مد گواهی رو هم روی Full بذارید.

<img width="1038" alt="cloudflare" src="https://user-images.githubusercontent.com/4588709/222557407-362ff8f2-fc33-462f-9449-5c00d93f6939.png">

این گزینه روشن باشه حتما

<img width="1034" alt="Bildschirm­foto 2023-03-02 um 00 08 26" src="https://user-images.githubusercontent.com/4588709/222558535-b264ff0b-9128-440c-ac85-9bb2bd8eb4a3.png">

این گزینه حتما روی TLS 1.3 باشه که میتونم بگم یکی از کلیدی‌ترین تنظیماتیه که باید رعایت بشه

<img width="1037" alt="Bildschirm­foto 2023-03-02 um 00 08 33" src="https://user-images.githubusercontent.com/4588709/222559477-050cc9ea-82ef-4dd3-a63f-17070e499332.png">

گزینه‌های زیر هم همگی روشن باشن

<img width="1037" alt="Bildschirm­foto 2023-03-02 um 00 08 45" src="https://user-images.githubusercontent.com/4588709/222559740-e3c0440a-51a7-4fc7-9016-b39993628106.png">

<img width="1040" alt="Bildschirm­foto 2023-03-02 um 00 09 04" src="https://user-images.githubusercontent.com/4588709/222560530-83a30252-99f1-4b10-ac5a-ebec1b114bfa.png">

#### Security
برای جلوگیری از سواستفاده از فیلترشکن از کشورهای دیگه حتما ترافیک ورودی به سمت سرور رو برای غیر از ایران ببندید.

<img width="1068" alt="Bildschirm­foto 2023-03-02 um 00 09 30" src="https://user-images.githubusercontent.com/4588709/222561693-cb3047c3-8cd6-40f4-ae03-263da3fda3aa.png">

حتما این مورد زیر رو هم Essenially off بذارید.

<img width="1042" alt="Bildschirm­foto 2023-03-02 um 00 09 46" src="https://user-images.githubusercontent.com/4588709/222562357-35598ffd-6632-4ec4-a100-ae00ccedec31.png">

موارد زیر هم من روشن گذاشتم

<img width="1041" alt="Bildschirm­foto 2023-03-02 um 00 09 56" src="https://user-images.githubusercontent.com/4588709/222562487-6c420f5d-98d0-4117-8646-da91137ebee0.png">

#### Network
گزینه‌های زیر روشن باشه.

<img width="1041" alt="Bildschirm­foto 2023-03-02 um 00 10 26" src="https://user-images.githubusercontent.com/4588709/222562740-769e6f1d-e66b-4e7e-a61b-a82a47bd6d97.png">

<img width="1037" alt="Bildschirm­foto 2023-03-02 um 00 10 36" src="https://user-images.githubusercontent.com/4588709/222562878-0838daec-896c-4ed1-8f4f-6bfa47f6df0d.png">

مورد زیر رو هم Add Header بذارید.

<img width="1034" alt="Bildschirm­foto 2023-03-02 um 00 10 46" src="https://user-images.githubusercontent.com/4588709/222563786-41a56558-8589-403b-a700-5e228375952e.png">

بقیه موارد رو هم تغییر ندادم و همون تنظیمات پیشنهادی خود کلادفلر گذاشتم.








