<div dir="rtl">

# TV Time Sync

برنامه‌ای سبک و مدرن برای **تلویزیون‌ها و باکس‌های اندرویدی** که ساعت و تاریخ دستگاه را با سرورهای زمان به‌روز می‌کند. اولویت همیشه با **سرورهای داخل ایران** است و اگر هیچ‌کدام پاسخ ندهند، سراغ سرورهای جهانی می‌رود.

![صفحه اصلی برنامه](screenshots/main.png)

> تصاویر این صفحه پیش‌نمایش رابط کاربری با داده نمونه هستند.

## چرا این برنامه؟

تلویزیون‌های اندرویدی ساعت خود را از سرور زمان گوگل می‌گیرند. وقتی این سرور در دسترس نباشد، ساعت و تاریخ دستگاه غلط می‌ماند و در نتیجه:

- سایت‌ها و برنامه‌ها خطای گواهی امنیتی (SSL) می‌دهند
- بعضی برنامه‌های پخش ویدیو و فروشگاه‌ها باز نمی‌شوند
- بعد از هر بار قطع برق، ساعت دوباره به‌هم می‌ریزد

TV Time Sync زمان درست را از سرورهای ایرانی می‌گیرد و روی دستگاه اعمال می‌کند.

## امکانات

- **اولویت با سرورهای ایران**: ۱۷ سرور NTP داخلی، بعد ۴۳ سرور جهانی
- **مسیر پشتیبان HTTP**: اگر پروتکل NTP بسته باشد، زمان از هدر پاسخ چند سایت ایرانی و جهانی خوانده می‌شود
- **اجرای خودکار هنگام روشن شدن** (انتخابی، پیش‌فرض خاموش)، بی‌صدا در پس‌زمینه
- **بدون نیاز به روت**
- نمایش ساعت، تاریخ میلادی، تاریخ شمسی و منطقه زمانی
- تست همه سرورها با نمایش تاخیر و اختلاف زمان هرکدام
- تنظیم منطقه زمانی روی تهران با یک دکمه
- طراحی‌شده برای کنترل تلویزیون (D-pad)
- رابط فارسی و انگلیسی (بر اساس زبان دستگاه)
- حجم حدود ۵۰ کیلوبایت، بدون هیچ کتابخانه جانبی، بدون تبلیغ و بدون جمع‌آوری اطلاعات

## پیش‌نیازها

- اندروید ۵ (API 21) یا بالاتر
- اتصال دستگاه به شبکه
- روشن بودن «USB debugging» در تنظیمات توسعه‌دهنده (فقط یک بار تنظیم می‌شود، پایین توضیح داده شده)

## نصب

۱. آخرین فایل `TVTimeSync-x.y.apk` را از بخش **Releases** همین مخزن دانلود کنید.

۲. فایل را به تلویزیون منتقل کنید. دو روش رایج:

- **فلش مموری**: فایل را روی فلش بریزید و با یک برنامه مدیریت فایل روی تلویزیون بازش کنید.
- **از طریق شبکه با ADB**:

```
adb connect TV_IP:5555
adb install TVTimeSync-1.0.apk
```

۳. اگر تلویزیون اجازه نصب نداد، در `Settings > Device Preferences > Security & restrictions > Unknown sources` به برنامه مدیریت فایل اجازه نصب بدهید.

## راه‌اندازی (فقط یک بار)

اندروید به برنامه‌های عادی اجازه تغییر ساعت سیستم را نمی‌دهد. این برنامه بدون روت و از طریق ADB داخلی خود دستگاه این کار را انجام می‌دهد، پس باید یک بار دیباگ را روشن کنید.

![راهنمای راه‌اندازی داخل برنامه](screenshots/setup-guide.png)

۱. به `Settings > Device Preferences > About` بروید و **۷ بار** روی گزینه «Build» بزنید تا پیام فعال شدن حالت توسعه‌دهنده را ببینید.

۲. به `Settings > Device Preferences > Developer options` بروید و «USB debugging» را روشن کنید. اگر گزینه «Network debugging» یا «ADB debugging» هم وجود دارد، آن را هم روشن کنید.

۳. برنامه TV Time Sync را باز کنید و دکمه **Sync now** را بزنید.

۴. تلویزیون پنجره «Allow USB debugging?» را نشان می‌دهد. تیک **Always allow from this computer** را بزنید و OK کنید. اگر این تیک را نزنید، اجرای خودکار هنگام روشن شدن کار نمی‌کند.

۵. در کادر وضعیت باید پیام به‌روز شدن ساعت را ببینید.

نام و محل این گزینه‌ها در برندهای مختلف کمی فرق دارد.

### اگر ADB محلی در دسترس نبود

در کادر وضعیت، عبارت `Local ADB (port 5555)` نشان می‌دهد که برنامه به ADB دستگاه دسترسی دارد یا نه. بعضی دستگاه‌های اندروید ۱۱ به بالا پورت 5555 را باز نمی‌کنند. در این حالت یک بار از کامپیوتری در همان شبکه این دستور را اجرا کنید:

```
adb connect TV_IP:5555
adb shell pm grant com.tvtimesync.app android.permission.WRITE_SECURE_SETTINGS
```

بعد از این کار برنامه سرور زمان خود اندروید را روی یک سرور ایرانی می‌گذارد و از سیستم می‌خواهد دوباره همگام شود. از این به بعد دیگر نیازی به ADB نیست.

## روش استفاده

| دکمه | کار |
|---|---|
| Sync now | زمان را از سرورها می‌گیرد و ساعت دستگاه را به‌روز می‌کند |
| Auto-run at boot | اجرای خودکار بعد از هر بار روشن شدن را روشن یا خاموش می‌کند |
| Test all servers | همه سرورها را تست می‌کند و نتیجه هرکدام را نشان می‌دهد |
| Set time zone to Tehran | منطقه زمانی را روی `Asia/Tehran` می‌گذارد |
| Setup guide | راهنمای راه‌اندازی را نمایش می‌دهد |

### اجرای خودکار

وقتی «Auto-run at boot» روشن باشد، برنامه بعد از بالا آمدن دستگاه بی‌صدا در پس‌زمینه اجرا می‌شود. اگر شبکه هنوز وصل نشده باشد، تا حدود دو دقیقه هر ۱۰ ثانیه دوباره تلاش می‌کند. فقط وقتی ساعت تغییر کند یا کار ناموفق باشد یک پیام کوتاه نشان داده می‌شود.

اگر دستگاه شما برنامه‌ها را بعد از بوت محدود می‌کند، برنامه را در تنظیمات بهینه‌سازی باتری یا اجرای خودکار مجاز کنید.

### تست سرورها

![تست سرورها](screenshots/server-test.png)

برای هر سرور، تاخیر رفت‌وبرگشت (rtt) و اختلاف ساعت دستگاه با آن سرور (offset) نمایش داده می‌شود. سرورهایی که پاسخ ندهند با `FAIL` مشخص می‌شوند.

## برنامه چطور کار می‌کند؟

۱. همه سرورهای NTP ایران هم‌زمان پرسیده می‌شوند.

۲. اگر هیچ‌کدام پاسخ ندهند، به ترتیب سراغ NTP جهانی، HTTP ایران و HTTP جهانی می‌رود.

۳. از بین پاسخ‌ها، آن‌هایی که با میانه بقیه بیش از ۳ ثانیه اختلاف دارند کنار گذاشته می‌شوند و کم‌تاخیرترین سرور انتخاب می‌شود.

۴. اگر اختلاف ساعت دستگاه کمتر از ۱٫۵ ثانیه باشد، چیزی تغییر نمی‌کند.

۵. در غیر این صورت ساعت به یکی از این دو روش اصلاح می‌شود:

- **روش مستقیم (ADB محلی)**: برنامه به `127.0.0.1:5555` وصل می‌شود و ساعت را با دستور `cmd alarm set-time` تنظیم می‌کند.
- **روش غیرمستقیم (مجوز WRITE_SECURE_SETTINGS)**: مقدار `ntp_server` اندروید روی سرور ایرانی گذاشته می‌شود و گزینه زمان خودکار خاموش و روشن می‌شود تا خود سیستم همگام شود.

۶. در پایان ساعت دوباره سنجیده می‌شود و اختلاف باقی‌مانده نمایش داده می‌شود.

## فهرست سرورها

### NTP ایران (اولویت اول)

<div dir="ltr">

```
ntp.time.ir
ntp.day.ir
ir.pool.ntp.org
0.ir.pool.ntp.org
1.ir.pool.ntp.org
2.ir.pool.ntp.org
3.ir.pool.ntp.org
ntp.iranet.ir
time1.iran.ir
ntp.snapp.ir
ntp.parsonline.com
ntp.ut.ac.ir
public.ntp.asiatech.ir
ntp.irimo.ir
194.225.150.25
2.188.16.51
185.204.197.106
```

</div>

### NTP جهانی

<div dir="ltr">

```
time.google.com            time1.google.com           time2.google.com
time3.google.com           time4.google.com           time.android.com
time.cloudflare.com        time.windows.com           time.apple.com
time.euro.apple.com        time.asia.apple.com        time.aws.com
time.facebook.com          time.nist.gov              utcnist.colorado.edu
tick.usno.navy.mil         tock.usno.navy.mil         pool.ntp.org
0.pool.ntp.org             1.pool.ntp.org             2.pool.ntp.org
3.pool.ntp.org             asia.pool.ntp.org          europe.pool.ntp.org
north-america.pool.ntp.org south-america.pool.ntp.org africa.pool.ntp.org
oceania.pool.ntp.org       tr.pool.ntp.org            ae.pool.ntp.org
de.pool.ntp.org            ru.pool.ntp.org            ntp.ubuntu.com
ntp.aliyun.com             ntp.tencent.com            ntp.ntsc.ac.cn
ntp.nict.jp                ptbtime1.ptb.de            ptbtime2.ptb.de
ntp.se                     ntp.time.nl                ntp1.hetzner.de
ntp.ripe.net
```

</div>

### پشتیبان HTTP

<div dir="ltr">

```
Iran:   time.ir, www.aparat.com, www.digikala.com, www.varzesh3.com
Global: www.google.com, www.cloudflare.com, www.microsoft.com, www.apple.com
```

</div>

برای افزودن یا حذف سرور، فایل `src/com/tvtimesync/app/Servers.java` را ویرایش و برنامه را دوباره بسازید.

## رفع اشکال

| پیام یا مشکل | راه‌حل |
|---|---|
| No time server answered | دستگاه به شبکه وصل نیست یا همه سرورها بسته‌اند. با «Test all servers» وضعیت را ببینید. |
| the app has no permission to change it | دیباگ روشن نیست یا تایید نشده. بخش «راه‌اندازی» را انجام دهید. |
| Local ADB port 5555 is closed | «USB debugging» را روشن کنید. اگر باز هم بسته بود، روش «اگر ADB محلی در دسترس نبود» را انجام دهید. |
| device requires TLS | دستگاه فقط Wireless debugging جدید را قبول می‌کند. از روش دستور `pm grant` با کامپیوتر استفاده کنید. |
| ADB authorization rejected | پنجره «Allow USB debugging» رد شده یا بسته شده. دوباره «Sync now» را بزنید و تایید کنید. |
| Time server was set, but the clock is still off | دستگاه تنظیم مستقیم را قبول نکرده و همگام‌سازی خود سیستم هنوز انجام نشده. چند دقیقه بعد دوباره امتحان کنید و مطمئن شوید «Automatic date & time» در تنظیمات دستگاه روشن است. |
| ساعت درست است ولی چند ساعت جلو یا عقب نمایش داده می‌شود | منطقه زمانی غلط است. دکمه «Set time zone to Tehran» را بزنید. |
| اجرای خودکار کار نمی‌کند | تیک «Always allow» را در پنجره دیباگ زده باشید و برنامه در تنظیمات اجرای خودکار دستگاه مجاز باشد. |

برای گزارش مشکل، متن کادر لاگ برنامه و مدل دستگاه و نسخه اندروید را در بخش Issues بنویسید.

## مجوزهای برنامه

| مجوز | دلیل |
|---|---|
| INTERNET | ارتباط با سرورهای زمان و ADB محلی |
| ACCESS_NETWORK_STATE | بررسی وضعیت شبکه |
| RECEIVE_BOOT_COMPLETED | اجرای خودکار هنگام روشن شدن |
| FOREGROUND_SERVICE و POST_NOTIFICATIONS | اجرای همگام‌سازی در پس‌زمینه |
| WRITE_SECURE_SETTINGS | تغییر سرور زمان سیستم (فقط با دستور `pm grant` فعال می‌شود) |
| SET_TIME_ZONE | تنظیم منطقه زمانی |

برنامه هیچ اطلاعاتی جمع‌آوری یا ارسال نمی‌کند. کلید ADB روی خود دستگاه ساخته می‌شود و فقط برای اتصال برنامه به همان دستگاه به کار می‌رود.

## نکته امنیتی

روشن بودن دیباگ شبکه یعنی هر دستگاهی در شبکه محلی می‌تواند درخواست اتصال ADB بفرستد. اتصال فقط بعد از تایید شما روی صفحه تلویزیون برقرار می‌شود، پس درخواست‌های ناشناس را تایید نکنید. اگر روش `pm grant` را انجام داده‌اید، می‌توانید بعد از آن دیباگ را خاموش کنید.

## ساخت از سورس

برنامه با جاوای خالص و بدون Gradle و بدون کتابخانه جانبی ساخته می‌شود.

پیش‌نیاز: JDK نسخه ۱۱ یا بالاتر، و از Android SDK بسته‌های `platforms;android-35` و `build-tools`.

<div dir="ltr">

```
git clone <repo-url>
cd tvtimesync
ANDROID_JAR=/path/to/sdk/platforms/android-35/android.jar \
BUILD_TOOLS=/path/to/sdk/build-tools/36.0.0 \
./build.sh
```

</div>

خروجی در `build/TVTimeSync-1.0.apk` ساخته می‌شود. در اولین اجرا یک کلید امضا به نام `release.jks` ساخته می‌شود. این فایل را نگه دارید و **در مخزن عمومی قرار ندهید**؛ نسخه‌های بعدی باید با همین کلید امضا شوند تا روی نسخه قبلی نصب شوند.

### ساختار پروژه

<div dir="ltr">

```
AndroidManifest.xml
build.sh                        build script
res/                            layout, strings (en + fa), drawables
src/com/tvtimesync/app/
  MainActivity.java             TV user interface
  SyncEngine.java               measure and apply logic
  Servers.java                  server lists
  NtpClient.java                SNTP client
  HttpTime.java                 HTTP Date fallback
  AdbClient.java, AdbCrypto.java   local ADB client
  BootReceiver.java, SyncService.java   auto-run at boot
  Jalali.java                   Persian calendar
test/                           fake NTP / ADB servers for testing
tools/render_previews.py        renders the README preview images
```

</div>

## سوالات متداول

**آیا به روت نیاز دارد؟**
نه. برنامه از ADB داخلی دستگاه یا مجوز `WRITE_SECURE_SETTINGS` استفاده می‌کند.

**روی گوشی هم کار می‌کند؟**
برنامه برای تلویزیون طراحی شده است. روی گوشی نصب می‌شود ولی صفحه فقط افقی است و ADB محلی روی گوشی‌ها معمولا در دسترس نیست.

**چرا برای مسیر پشتیبان از HTTP ساده استفاده می‌شود و نه HTTPS؟**
وقتی ساعت دستگاه غلط باشد، بررسی گواهی HTTPS شکست می‌خورد. برای همین زمان از هدر `Date` پاسخ HTTP ساده خوانده می‌شود. دقت این روش حدود یک ثانیه است.

**ساعت بعد از قطع برق دوباره غلط می‌شود؟**
«Auto-run at boot» را روشن کنید تا بعد از هر بار روشن شدن خودکار اصلاح شود.

</div>
