

<div dir="rtl" markdown=1>
# نحوه تنظیم و استفاده از ورکرز

## ورکرز چیست؟
ورکرز یکی از سرویس های CDN معروف Cloudflare است که در واقع یک سرویس بدون سرور یا Serverless می باشد و از طریق آن می‌توان کدهای برنامه نویسی را اجرا نمود بدون آنکه نیاز به پیکربندی سرور و یا زیرساخت باشد. در حقیقت این سرویس یک نوع رایانش ابری مبتی بر SaaS می باشد. 

به عبارت دیگه روش کار ورکرز بدین صورت است که به جای اینکه بخواهید مستقیما وبسایت خود (در اینجا پنل هیدیفای) را باز نمایید؛ درخواست ها را به ورکرز می فرستید و سپس ورکرز درخواست ها را مجددا به سمت دامنه و سرور شما ارسال می کند.


![](https://user-images.githubusercontent.com/125398461/224561104-dafc3e89-1c0d-4afc-82eb-cce1cec6933a.png)

در اینجا هدف از این کار مخفی کردن دامنه پشت ورکرز است.

## چگونه از ورکرز استفاده کنید؟
برای استفاده از ورکرز نیاز دارید که یک دامنه فعال روی کلادفلر داشته باشید.

## ثبت دامنه و زیر دامنه روی کلادفلر
در اینجا به یک دامنه خریداری شده نیاز دارید و نیاز دارید که آن را در کلادفلر ثبت نمایید.
اگر در خصوص دامنه و نحوه ثبت آن ابهامی دارید؛ [این مطلب](/manager/wiki/%D8%A7%D9%86%D9%88%D8%A7%D8%B9-%D8%AF%D8%A7%D9%85%D9%86%D9%87-%D9%88-%D9%86%D8%AD%D9%88%D9%87-%D8%AB%D8%A8%D8%AA-%E2%80%8C%D8%A2%D9%86%E2%80%8C%D9%87%D8%A7) را مطالعه کنید.

طبق توضیحات مربوط به نحوه ثبت دامنه وارد اکانت خود در کلادفلر شوید.

![221572305-50e819ea-0fa4-4548-8851-aab91b797f57](https://user-images.githubusercontent.com/125398461/224561629-dd0be4b5-9345-43b7-aa81-a3bfaaaf5899.png)


وارد دامنه ثبت شده شوید و در قسمت DNS یک زیردامنه جدید ثبت نمایید.

![](https://user-images.githubusercontent.com/125398461/224561952-cbb99885-46f7-49e2-874d-f48e5b0c9b0d.png)


> الزامی وجود ندارد که پروکسی روشن باشد. ورکرز با هر دو حالت پروکسی روشن و خاموش کار می کند.

![](https://user-images.githubusercontent.com/125398461/224562373-5201f8b6-5d5c-492f-a6b9-9c4366d4f9db.png)

پس از ثبت ساب دامنه باید تنظیمات سرتیفیکت را انجام دهید..

## تنظیم سرتیفیکت دامنه
در تنظیمات سرتیفیکت دامنه در سایت کلادفلر بروید و سرتیفیکت را روی `Full` بگذارید.
</div>

<div align=center markdown=1>
![](https://user-images.githubusercontent.com/125398461/235835085-8d9c9ea5-16f2-4782-bfa2-4cc010d7367c.png)

</div>

<div dir="rtl" markdown=1>
## ساخت سرویس ورکرز

به بخش ورکرز در صفحه داشبورد خود در کلادفلر بروید.

![](https://user-images.githubusercontent.com/125398461/224562657-f433fff0-d4a1-4fe6-95e0-5f4e17337c3d.png)

سپس گزینه Create a Service را انتخاب نمایید.

![Screenshot_20230312_211625](https://user-images.githubusercontent.com/125398461/224562813-20dc1a02-8d93-446b-a7d9-d90fbae3cda3.png)

در اینجا شما می توانید نام سرویس ورکرز خود را انتخاب نمایید. کلادفلر خود نیز یک نام به شما پیشنهاد می دهد. می توانید آن را تغییر دهید اما توجه داشته باشید که این نام باید منحصر به فرد باشد.

![](https://user-images.githubusercontent.com/125398461/224563236-dc4c5497-b179-46f4-ae53-9c003d3789d6.png)


گزینه Starter نیز روی HTTP handler  باشد. در آخر با انتخاب Create service سرویس ورکرز شما ایجاد می گردد.

بعد از آن باید روی دکمه Quick edit کلیک کنید تا بتوانید کد دلخواه خود را در ورکرز قرار دهید.


![](https://user-images.githubusercontent.com/125398461/224563711-3675b1dc-5f50-4c34-94b3-d47f5a00f7c8.png)

در صفحه ادیت ورکرز قسمت سمت چپ کدهای دیفالت را پاک کنید.

![](https://user-images.githubusercontent.com/125398461/224564027-10fb94b7-770f-4a44-82e6-c414469a72f4.png)

سپس کد زیر را به جای آن قرار دهید.

</div>

```
addEventListener(
   "fetch", event => {
       
       const ip = event.request.headers.get('cf-connecting-ip') || event.request.headers.get('x-forwarded-for') || (event.request.socket && event.request.socket.remoteAddress);
       let url = new URL(event.request.url);
       const worker_domain=url.hostname;
       url.hostname = "sub.domain.com";                        
       url.protocol = event.request.headers.get('x-forwarded-proto') || "https";
       let request = new Request(url, event.request);
       if (ip)
        request.headers.set('cf-connecting-ip', ip);
        request.headers.set('Host', worker_domain);
       event.respondWith(
           fetch(request)
       )
   }
)
```

<div dir="rtl" markdown=1>
> دقت شود:
* در خط ششم باید دامنه ثبت شده در مرحله اول را برای مقدار `url.hostname` قرار دهید.
یعنی مثلا ساب دامین `sub.domain.com` را در کلادفلر طبق توضیحات مرحله اول ثبت کرده‌اید؛ در اینجا نیاز دارید آن دامنه را برای مقدار `url.hostname` قرار دهید.

![final_status](https://user-images.githubusercontent.com/125398461/232571080-6e001a84-ec55-42f1-b424-e592a57a4212.png)



دکمه Save and deploy را کلیک کنید.

**نکته خیلی مهم: اگر در مرحله ذخیره کد در قسمتی که نتیجه اجرای کد را نمایش می دهد (که در تصویر بالا سمت راست تصویر مشخص شده) خطایی نمایش داد نگران نباشید. کد را ذخیره کنید.**

در صفحه ورکرز آدرس ورکرز خود را بدون `https` کپی کنید. مثلا اینطوری:

![](https://user-images.githubusercontent.com/125398461/224895042-d6a4e78b-f98f-4b9f-b6ad-a733eff3213a.png)

این مرحله با موفقیت به اتمام رسید. حالا باید آدرس سرویس ورکرز خود را در پنل هیدیفای ثبت کنید.

### ثبت ورکرز در هیدیفای

به منوی دامنه ها بروید و روی ایجاد کلیک کنید.




![](https://user-images.githubusercontent.com/125398461/224565137-834f8fbb-5d8f-4fd0-bf98-0571fed2e542.png)

تنظیمات را مطابق با عکس بالا انجام دهید و ذخیره نمایید.

> توجه: از هر دو حالت CDN و AutoCDN می‌توانید برای ورکرز استفاده کنید.

کار تمام شد. یک دامنه CDN با مشخصات ورکرز شما به دامین های قبلی شما اضافه شد و می توانید از کانکشن های آن استفاده نمایید.



> نکته پایانی و مهم:
*  ورکرز در پلن رایگان به صورت روزانه فقط ۱۰۰ هزار درخواست را پردازش می کند بنابراین این سرویس به درد کسانی میخورد که ترافیک بالایی روی سرور خود ندارند.

</div>

<div align=center markdown=1>
![](https://user-images.githubusercontent.com/125398461/235835675-e454ba05-29ad-4b53-9cf9-f23f4c225ef6.png)


</div>

<div dir="rtl" markdown=1>
## اضافه کردن کانفیگ‌های ورکرز به دامین مربوط به لینک‌های سابسکریپشن


همانطور که احتمالا می‌دانید، در هیدیفای شما می‌توانید لینک‌های سابسکریپشن را روی یک دامنه مجزا قرار دهید و دامنه‌های دیگر که برای کانکشن‌ها تنظیم شده است را به این دامنه اضافه نمایید. مزیت این کار این است که همیشه دامنه لینک‌ها در دسترس خواهد بود و فیلتر نخواهد شد چون با این روش، کانکشن‌ها  از لینک‌های سابسکریپشن جدا می‌شوند. 

خب فرض کنید دامنه لینک‌های سابسکریپشن ما که قبلا ثبت نموده اید، `t1.hiddify.com` باشد. به تنظیمات مربوط به این دامنه بروید و در فیلد نمایش کانفیگ‌های دامنه، دامنه جدیدی که در مرحله قبل برای ورکرز اضافه نموده بودید را مثل شکل زیر تیک بزنید.

![](https://github.com/hiddify/hiddify-config/assets/125398461/b5fa6070-167b-4143-a4d4-3247fb78f735)

در نهایت اگر به صفحه کاربران بروید و مثل شکل زیر روی لینک کاربر کلیک کنید،

![](https://github.com/hiddify/hiddify-config/assets/125398461/11489c60-e89a-445b-9281-270959869e30)

خواهید دید که کانفیگ‌های جدید مربوط به ورکرز به کانفیگ‌های قبلی اضافه شده‌اند.


![Screen Shot 1402-02-29 at 10 46 16](https://github.com/hiddify/hiddify-config/assets/125398461/25ba5f2e-b309-47ad-ad98-35edea4feb83)


