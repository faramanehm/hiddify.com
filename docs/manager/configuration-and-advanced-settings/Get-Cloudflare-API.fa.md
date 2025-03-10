
<div dir="rtl" markdown=1>
# گرفتن کلید توسعه کلودفلر

هدف از این کار اتصال پنل به کلادفلر است. با انجام این کار وقتی در پنل ساب‌دامین ایجاد می‌نمایید؛ کلادفلر به صورت خودکار آن‌ها را می‌سازد و برایشان سرتیفیکت می‌گیرد. همچنین پروسه ساخت ورکرز خودکار می‌گردد. مراحل زیر را به ترتیب انجام دهید تا توکن مربوط به کلید توسعه کلودفلر را دریافت کنید.

۱. قبل از هر چیز وارد اکانت خود در کلادفلر شوید و دامنه خود را ثبت نمایید. اگر نیاز به اطلاعات بیشتر برای این کار دارید لطفا [این لینک](/manager/wiki/%D8%A7%D9%86%D9%88%D8%A7%D8%B9-%D8%AF%D8%A7%D9%85%D9%86%D9%87-%D9%88-%D9%86%D8%AD%D9%88%D9%87-%D8%AB%D8%A8%D8%AA-%E2%80%8C%D8%A2%D9%86%E2%80%8C%D9%87%D8%A7) را مطالعه کنید.

۲. از [اینجا](https://dash.cloudflare.com/profile/api-tokens/)، به **My Profile** > **API Tokens** بروید.
    
۳. `Create Token` را انتخاب کنید.

    
![](https://user-images.githubusercontent.com/125398461/234880340-5f1abcac-9f10-46eb-bb19-204546e3c453.png)


۴. یک الگو از میان الگوهای موجود انتخاب کنید یا یک نشانه سفارشی ایجاد کنید. ما پیشنهاد می‌کنیم از الگوی `Edit zone DNS` همانند مثال زیر استفاده کنید.

![](https://user-images.githubusercontent.com/125398461/234880943-80462114-58bd-48df-baef-2addfc740062.png)

    



۵.  در این مرحله تنظیمات دسترسی و منابع Zone را به شکل زیر انجام دهید.


![](https://user-images.githubusercontent.com/125398461/235046796-2ea8d0ed-4fe4-4060-ae55-683c9d2c0e7c.png)

<!--   
![صفحه نمای کلی الگوی رمز](https://user-images.githubusercontent.com/114227601/229591958-adc4e813-1e04-4de0-9bbb-29b94df4b4d9.png)
-->
می‌توانید مجوزهای توکن را از بین (_Account_، _User_، یا _Zone_) تغییر دهید. اکثر گروه‌ها گزینه‌های «ویرایش» یا «خواندن» را ارائه می‌کنند. «ویرایش» دسترسی کامل CRUDL (ایجاد، خواندن، به‌روزرسانی، حذف، فهرست) است، در حالی که «خواندن» در صورت لزوم مجوز خواندن و فهرست است. برای اطلاعات بیشتر به [مجوزهای نشانه موجود](/fundamentals/api/reference/permissions/) مراجعه کنید. 

برای اعمال تغییرات روی دامین‌ها و ورکرزهای خود به ترتیب زیر جلو بروید.

* مجوز `Zone` را روی `DNS` و در حالت `Edit` باشد تا امکان اضافه کردن ساب‌دامین‌های مختلف داده شود.

* دکمه Add more را بزنید و در قسمت `Account` گزینه `Workers Scripts` را انتخاب کنید و به آن مجوز Edit دهید.

* در بخش `Account Resources` گزینه `All accounts` را انتخاب نمایید.

* در قسمت `Zone Resources` منابع را به اکانت خود تخصیص دهید. یعنی `All zones from an account` را انتخاب نمایید و سپس اکانت کلادفلر خود را انتخاب کنید.

* در آخر `Continue to summary` را بزنید.
  
۶. برای ایجاد توکن `Create Token` را انتخاب کنید.

![صفحه نمایش خلاصه نشانه با نمایش منابع و مجوزهای انتخاب شده](https://user-images.githubusercontent.com/114227601/229592071-3faf93c3-b246-4a08-823b-4680a3a4cf5e.png)

    

    
۷. توکن را کپی کنید.

![229592139-25482e17-ddef-48b5-9926-265d073669e9](https://user-images.githubusercontent.com/125398461/234892482-293f7505-5c94-4564-b0d6-3337fd435e7c.png)


# استفاده از کلید توسعه کلادفلر در پنل

بعد از ایجاد توکن؛ وارد پنل شوید و در تنظیمات خیلی پیشرفته؛ توکن را در فیلد مشخص شده مطابق با تصویر زیر جایگذاری کنید.

![Screenshot_20230427_1758442](https://user-images.githubusercontent.com/125398461/234895891-9a0f71a5-86fd-423c-86a6-3c3acf50818e.png)

حالا اگه در قسمت دامنه‌ها در پنل یک ساب‌دامین جدید روی دامین ثبت شده خود در کلادفلر ایجاد نمایید؛ تنظیمات بخش کلودفلر به صورت خودکار انجام می‌شود. همچنین ورکرز به صورت خودکار ساخته می‌شود.

</div>