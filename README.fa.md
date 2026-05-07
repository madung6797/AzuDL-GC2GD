# AzuDl - GC2GD

<p align="center">
  <strong>فارسی</strong> · <a href="README.md">English</a>
</p>

<p align="center">
  <strong>Azizi Universal Downloader - Google Colab to Google Drive</strong>
</p>

<p align="center">
  یک دانلودر و ابزار مدیریت فایل قدرتمند برای Google Colab که خروجی را مستقیم داخل Google Drive ذخیره می‌کند.
</p>

<p align="center">
  <code>Google Colab</code> · <code>Google Drive</code> · <code>aria2</code> · <code>yt-dlp</code> · <code>FFmpeg</code> · <code>Python</code>
</p>

---

## معرفی

**AzuDl - GC2GD** مخفف عبارت زیر است:

> **Azizi Universal Downloader - Google Colab to Google Drive**

این پروژه یک ابزار دانلود برای Google Colab است که فایل‌ها و محتوای پشتیبانی‌شده را مستقیم داخل Google Drive ذخیره می‌کند.

نسخه **1.2.0** نسخه کامل‌تر پروژه است و قابلیت‌هایی مثل مدیریت بهتر تورنت، پشتیبانی از فایل `.torrent`، هدر اختصاصی برای لینک مستقیم، ذخیره metadata و thumbnail یوتیوب، گزارش فضای Drive، محاسبه SHA256، ساخت ZIP و مدیریت aria2 به آن اضافه شده است.

---

## برای کاربران عادی

اگر می‌خواهی فایل‌ها را بدون روشن نگه داشتن سیستم شخصی دانلود کنی، این ابزار برای همین ساخته شده است.

Google Colab را باز می‌کنی، کد را اجرا می‌کنی، Google Drive را وصل می‌کنی و لینک را وارد می‌کنی. فایل نهایی مستقیم داخل Drive ذخیره می‌شود.

با AzuDl می‌توانی:

- لینک مستقیم دانلود کنی
- ویدیو از YouTube دانلود کنی
- پلی‌لیست YouTube دانلود کنی
- صدای YouTube را به MP3 تبدیل کنی
- Magnet Torrent دانلود کنی
- فایل `.torrent` دانلود کنی
- چند لینک را پشت سر هم دانلود کنی
- پوشه‌های دانلودشده را ZIP کنی
- سلامت فایل را با SHA256 بررسی کنی

---

## برای برنامه‌نویس‌ها

هسته پروژه بر اساس یک کلاس پایتونی نوشته شده است:

```python
class AzuDlGC2GD:
```

این کلاس مدیریت می‌کند:

- اتصال Google Drive
- ساخت پوشه‌های پروژه
- اجرای aria2 در حالت RPC
- ارتباط با aria2 از طریق JSON-RPC
- تشخیص metadata در Magnet
- پیدا کردن GID واقعی تورنت بعد از metadata
- بارگذاری فایل `.torrent` با `aria2.addTorrent`
- دانلود لینک مستقیم با aria2
- دانلود YouTube با `yt-dlp`
- نمایش Progress با `tqdm.notebook`
- ثبت تاریخچه دانلودها
- گزارش فضای ذخیره‌سازی
- محاسبه SHA256
- ساخت ZIP
- مدیریت taskهای aria2

---

## قابلیت‌ها

### قابلیت‌های دانلود

- دانلود Magnet Torrent
- نمایش Progress واقعی تورنت بعد از metadata
- دانلود فایل `.torrent` از URL یا مسیر لوکال
- دانلود لینک مستقیم
- پشتیبانی از Header اختصاصی برای لینک مستقیم
- دانلود ویدیو از YouTube
- دانلود پلی‌لیست YouTube
- استخراج صدا از YouTube به MP3
- انتخاب کیفیت YouTube
- پشتیبانی از Custom Format ID
- ذخیره اختیاری metadata و thumbnail برای YouTube
- دانلود گروهی یا Batch Download
- محدودیت سرعت برای دانلودهای aria2
- پشتیبانی از ادامه دانلود

### ابزارهای فایل

- نمایش فایل‌های دانلودشده
- نمایش آخرین فایل دانلودشده
- گزارش فضای Google Drive
- گزارش حجم پوشه‌های پروژه
- محاسبه SHA256 برای آخرین فایل
- محاسبه SHA256 برای فایل انتخابی
- ZIP کردن یک پوشه
- ZIP کردن آخرین پوشه دانلودشده
- ذخیره تاریخچه دانلودها

### ابزارهای aria2

- نمایش دانلودهای Active، Waiting و Stopped
- حذف دانلود با GID
- پاک‌سازی نتایج Stopped
- نمایش بهتر وضعیت تورنت
- نمایش درصد، سرعت، تعداد اتصال‌ها و Seederها

---

## منوی برنامه

```text
1. Auto detect link
2. Torrent magnet
3. Torrent file
4. YouTube video or playlist
5. Direct link
6. Batch download
7. Download history
8. List downloaded files
9. Storage report
10. SHA256 latest file
11. SHA256 selected file
12. ZIP folder
13. ZIP latest folder
14. aria2 status
15. Remove aria2 GID
16. Clear stopped aria2 results
17. Latest file
18. Developer
19. Help
20. Exit
```

---

## ساختار پوشه‌ها

پروژه این مسیر را داخل Google Drive می‌سازد:

```text
/content/drive/MyDrive/AzuDl-GC2GD
```

ساختار:

```text
AzuDl-GC2GD/
├── TorrentDownloads/
├── YouTubeDownloads/
├── DirectDownloads/
├── BatchDownloads/
├── Archives/
└── Logs/
    └── download_history.json
```

| پوشه | کاربرد |
|---|---|
| `TorrentDownloads` | دانلودهای Magnet و `.torrent` |
| `YouTubeDownloads` | ویدیو، پلی‌لیست، صدا، metadata و thumbnail یوتیوب |
| `DirectDownloads` | دانلودهای لینک مستقیم |
| `BatchDownloads` | دانلودهای گروهی |
| `Archives` | فایل‌های ZIP ساخته‌شده |
| `Logs` | تاریخچه دانلود و لاگ‌ها |

---

## آپدیت مهم تورنت در v1.2.0

Magnet در aria2 چند مرحله دارد:

```text
Magnet link
  ↓
دریافت metadata
  ↓
ساخت task واقعی تورنت
  ↓
دانلود فایل اصلی
```

در نسخه‌های قبلی ممکن بود فقط metadata نمایش داده شود:

```text
Torrent: 100% 5.77k/5.77k
```

این فایل اصلی نبود؛ فقط metadata تورنت بود.

نسخه **1.2.0** بعد از دریافت metadata، `GID` واقعی دانلود تورنت را پیدا می‌کند و Progress فایل اصلی را نمایش می‌دهد.

خروجی درست باید شبیه این باشد:

```text
Magnet added
Metadata GID: ...
Fetching metadata: 100%
Metadata completed
Real torrent GID: ...
Starting torrent download monitor
Torrent Download: ...
```

---

## دانلود Magnet

از منو انتخاب کن:

```text
2. Torrent magnet
```

بعد Magnet را وارد کن:

```text
magnet:?xt=urn:btih:EXAMPLE_HASH
```

نمونه محدودیت سرعت:

```text
500K
2M
10M
```

---

## دانلود فایل torrent

از منو انتخاب کن:

```text
3. Torrent file
```

می‌توانی URL فایل `.torrent` را بدهی:

```text
https://example.com/file.torrent
```

یا مسیر فایل داخل Colab/Drive را وارد کنی:

```text
/content/drive/MyDrive/file.torrent
```

---

## دانلود از YouTube

از منو انتخاب کن:

```text
4. YouTube video or playlist
```

نمونه لینک‌ها:

```text
https://www.youtube.com/watch?v=VIDEO_ID
https://youtu.be/VIDEO_ID
https://www.youtube.com/playlist?list=PLAYLIST_ID
https://music.youtube.com/watch?v=VIDEO_ID
```

کیفیت‌های آماده:

```text
best
4320
2160
1440
1080
720
480
360
```

نمونه Custom Format:

```text
137+140
248+251
22
18
best
```

در حالت Audio Only خروجی MP3 ذخیره می‌شود.  
در حالت metadata، فایل `.info.json` و thumbnail هم ذخیره می‌شود.

---

## دانلود لینک مستقیم

از منو انتخاب کن:

```text
5. Direct link
```

پروتکل‌های پشتیبانی‌شده:

```text
http://
https://
ftp://
```

گزینه‌های اختیاری:

```text
Folder name
File name
Speed limit
Headers JSON
```

نمونه Header:

```json
{"User-Agent":"Mozilla/5.0","Referer":"https://example.com"}
```

---

## دانلود گروهی

از منو انتخاب کن:

```text
6. Batch download
```

لینک‌ها را یکی‌یکی وارد کن. با خط خالی، دانلود شروع می‌شود.

Batch از این لینک‌ها پشتیبانی می‌کند:

- Magnet
- فایل `.torrent`
- YouTube
- لینک مستقیم

---

## گزارش فضای ذخیره‌سازی

از منو انتخاب کن:

```text
9. Storage report
```

نمایش می‌دهد:

- کل فضای Mount شده
- فضای استفاده‌شده
- فضای آزاد
- حجم هر پوشه پروژه

---

## SHA256

برای آخرین فایل:

```text
10. SHA256 latest file
```

برای انتخاب فایل:

```text
11. SHA256 selected file
```

SHA256 برای بررسی سلامت فایل بعد از دانلود کاربرد دارد.

---

## ابزار ZIP

برای ZIP کردن یک پوشه:

```text
12. ZIP folder
```

برای ZIP کردن آخرین پوشه دانلودشده:

```text
13. ZIP latest folder
```

خروجی‌ها اینجا ذخیره می‌شوند:

```text
/content/drive/MyDrive/AzuDl-GC2GD/Archives
```

---

## ابزارهای aria2

برای مشاهده وضعیت دانلودها:

```text
14. aria2 status
```

برای حذف یک دانلود با GID:

```text
15. Remove aria2 GID
```

برای پاک‌سازی نتایج متوقف‌شده:

```text
16. Clear stopped aria2 results
```

---

## تاریخچه دانلودها

تاریخچه اینجا ذخیره می‌شود:

```text
/content/drive/MyDrive/AzuDl-GC2GD/Logs/download_history.json
```

نمونه:

```json
{
  "type": "youtube",
  "source": "https://www.youtube.com/watch?v=VIDEO_ID",
  "output": "/content/drive/MyDrive/AzuDl-GC2GD/YouTubeDownloads/Example",
  "format": "bv*+ba/best",
  "status": "completed",
  "time": "2026-05-06 18:30:00"
}
```

---

## نصب و اجرا

کل سورس پروژه را داخل یک سلول Google Colab قرار بده و اجرا کن.

وابستگی‌ها:

```text
aria2
ffmpeg
p7zip-full
tqdm
requests
yt-dlp
```

---

## رفع خطاهای رایج

### Google Drive وصل نمی‌شود

اول Runtime را Restart کن:

```text
Runtime > Restart session
```

یا اجرا کن:

```python
from google.colab import drive
drive.flush_and_unmount()
```

بعد دوباره Runtime را Restart کن.

راهکارهای دیگر:

- فقط با یک اکانت گوگل وارد باش
- از Incognito استفاده کن
- Third-party cookies را فعال کن
- Drive را از پنل فایل‌های Colab دوباره وصل کن

### تورنت metadata می‌گیرد ولی دانلود اصلی شروع نمی‌شود

دلایل احتمالی:

- Seeder ندارد
- Peer کافی پیدا نشده
- تورنت ضعیف است
- محدودیت شبکه وجود دارد

برای بررسی:

```text
14. aria2 status
```

### YouTube دانلود نمی‌شود

برای آپدیت yt-dlp:

```python
!pip install -U yt-dlp
```

### لینک مستقیم دانلود نمی‌شود

دلایل احتمالی:

- لینک منقضی شده
- Header نیاز دارد
- سرور Colab را بلاک کرده
- Authentication لازم دارد
- Token موقت تمام شده

در این حالت Headers JSON را امتحان کن.

---

## استفاده مسئولانه

AzuDl فقط یک ابزار دانلود و مدیریت فایل است.  
از آن فقط برای فایل‌ها و محتواهایی استفاده کن که اجازه دانلود، ذخیره یا پردازش آن‌ها را داری.

نمونه‌های مناسب:

- فایل‌های شخصی
- پروژه‌های Open Source
- محتوای Public Domain
- محتوای Creative Commons
- بکاپ اطلاعات خودت
- فایل‌هایی که صاحب اثر اجازه دانلودشان را داده

از این ابزار برای نقض کپی‌رایت، دور زدن محدودیت دسترسی یا دانلود محتوای غیرمجاز استفاده نکن.

---

## برنامه‌نویس

**Project:** AzuDl - GC2GD  
**Full Name:** Azizi Universal Downloader - Google Colab to Google Drive  
**Developer:** The Azizi

### لینک‌ها

- X: https://x.com/the_azzi
- GitHub: https://github.com/TheGreatAzizi
- Telegram: https://t.me/luluch_code
- Git: https://git.theazizi.ir/TheAzizi
- Website: https://theazizi.ir

---

## نسخه

```text
Current version: 1.2.0
```
