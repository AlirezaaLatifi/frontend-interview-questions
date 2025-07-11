---
title: تایپ اسکریپت و جاوااسکریپت
---

<link rel="stylesheet" href="{{ site.baseurl }}/assets/css/persian.css">

### 1. حلقه رویداد جاوااسکریپت چگونه کار می‌کند و چه تأثیری بر رندر و به‌روزرسانی‌های وضعیت React دارد؟

حلقه رویداد به جاوااسکریپت (تک‌ریسمانی) امکان مدیریت **عملیات‌های غیرهمزمان** را با استفاده از **پشته فراخوانی**، **صف وظایف (ماکروتسک‌ها)** و **صف میکروتسک‌ها** می‌دهد.

در React:

- `setState` **دسته‌بندی‌شده و غیرهمزمان** است.
- به‌روزرسانی‌های وضعیت و رندر **پس از خالی شدن پشته فراخوانی فعلی** انجام می‌شوند (به‌عنوان میکروتسک یا ماکروتسک در صف قرار می‌گیرند بسته به زمینه).
- درک این موضوع از شرایط رقابتی جلوگیری کرده و اطمینان می‌دهد که به‌روزرسانی‌های رابط کاربری به‌صورت قابل پیش‌بینی رخ می‌دهند.

<br />

### 2. مدل ذهنی شما برای درک کلوژرهای جاوااسکریپت چیست و چگونه از آن‌ها به‌طور مؤثر در یک برنامه React استفاده می‌کنید؟

کلوژر تابعی است که **به حوزه لغوی خود دسترسی حفظ می‌کند**، حتی زمانی که خارج از آن حوزه فراخوانی شود.

در React:

- برای **بازگشت‌های مموایز شده** یا مدیریت **وضعیت محصور شده** در هوک‌های سفارشی مفید است.

کلوژرها باید در افکت‌ها با دقت مدیریت شوند تا از مشکلات **وضعیت قدیمی** جلوگیری شود.

<br />

### 3. ارث‌بری پروتوتایپی در جاوااسکریپت را چگونه توضیح می‌دهید و چگونه با ارث‌بری کلاسیک متفاوت است؟

ارث‌بری پروتوتایپی اشیاء را از طریق **زنجیره [[Prototype]]** به یکدیگر متصل می‌کند و امکان اشتراک ویژگی‌ها را فراهم می‌کند.

برخلاف ارث‌بری کلاسیک:

- جاوااسکریپت **واگذاری شیء را به جای سلسله‌مراتب کلاس‌ها** ترجیح می‌دهد.
- **پویاتر و انعطاف‌پذیرتر** است، که به‌خوبی با **الگوهای ترکیبی** در React هم‌خوانی دارد.

<br />

### 4. اهمیت کلمه کلیدی `this` در جاوااسکریپت چیست و چگونه اتصال آن را در کامپوننت‌های React مدیریت می‌کنید؟

`this` به **زمینه اجرا** اشاره دارد. در کامپوننت‌های کلاسی React، `this` اغلب به **نمونه کامپوننت** اشاره می‌کند.

در کامپوننت‌های کلاسی:

```jsx
this.handleClick = this.handleClick.bind(this);
```

در کامپوننت‌های تابعی:

- از `this` به‌طور کامل با استفاده از هوک‌ها و توابع پیکانی اجتناب می‌کنم.
- توابع پیکانی `this` را به‌صورت **لغوی متصل می‌کنند**.

<br />

### 5. ماهیت تک‌ریسمانی جاوااسکریپت چگونه بر رویکرد شما برای مدیریت وظایف محاسباتی سنگین در یک برنامه React تأثیر می‌گذارد؟

از آنجا که جاوااسکریپت روی یک **ریسمان واحد** اجرا می‌شود، وظایف سنگین **رابط کاربری را مسدود می‌کنند**.

استراتژی‌ها:

- **وب ورکرها** برای انتقال کارهای سنگین CPU.
- **محدود کردن/تاخیر دادن** ورودی‌ها.
- استفاده از **`requestIdleCallback`** یا `setTimeout` برای به تعویق انداختن کار.
- نگه داشتن کامپوننت‌ها **خالص و سریع در رندر**.

<br />

### 6. چگونه یک جریان کاری async/await قوی در یک برنامه React برای مدیریت چندین فراخوانی API طراحی می‌کنید؟

استفاده از `async/await` داخل `useEffect`، محصور در `try/catch`، و به‌صورت اختیاری استفاده از `Promise.all`.

<br />

### 7. تفاوت بین پرامیس‌ها و async/await در زیرساخت چیست و چگونه استفاده آن‌ها را در React بهینه می‌کنید؟

- **پرامیس‌ها** مقادیر غیرهمزمان را نشان می‌دهند؛ `then` بازگشت‌ها را زنجیره می‌کند.
- `async/await` **شکر سینتکسی** روی پرامیس‌هاست که خوانایی و اشکال‌زدایی را بهبود می‌بخشد.

بهینه‌سازی‌ها:

- اجتناب از `await` تودرتو در حلقه‌ها (استفاده از `Promise.all`).
- مموایز کردن توابع غیرهمزمان با `useCallback`.
- همیشه **پاکسازی** را در افکت‌های غیرهمزمان مدیریت کنید تا از شرایط رقابتی جلوگیری شود.

<br />

### 8. چگونه یک ابزار مبتنی بر پرامیس سفارشی (مثل مکانیزم تلاش مجدد) برای یک برنامه React پیاده‌سازی می‌کنید؟

```jsx
const retry = (fn, retries = 3, delay = 1000) =>
  fn().catch((err) => {
    if (retries === 0) throw err;
    return new Promise((res) => setTimeout(res, delay)).then(() =>
      retry(fn, retries - 1, delay)
    );
  });
```

<br />

### 9. چگونه میکروتسک‌ها و ماکروتسک‌ها را در یک برنامه React با عملیات‌های غیرهمزمان سنگین مدیریت می‌کنید؟

- **میکروتسک‌ها**: پرامیس‌ها، `queueMicrotask`.
- **ماکروتسک‌ها**: `setTimeout`، `fetch`.

از **میکروتسک‌ها برای زنجیره‌بندی منطق** و **ماکروتسک‌ها برای به تعویق انداختن** اجرا استفاده کنید.

<br />

### 10. چگونه از پروتکل ایتراتور غیرهمزمان (مثل `for await...of`) در یک برنامه React برای داده‌های جریانی استفاده می‌کنید؟

برای **APIهای جریانی** (مثل SSE، تکه‌های فایل) استفاده می‌شود:

```jsx
async function streamData(url) {
  const response = await fetch(url);
  for await (const chunk of response.body) {
    processChunk(chunk);
  }
}
```

در React:

- اجرا داخل `useEffect`.
- برای **فیدهای بلادرنگ یا دانلودهای طولانی** مفید است.

<br />

### 11. چگونه از ماژول‌های ES6 در یک کدبیس بزرگ React برای اطمینان از قابلیت نگهداری و tree-shaking استفاده می‌کنید؟

- استفاده از **صادرات نام‌گذاری‌شده** برای tree-shaking بهتر.
- ساختاردهی ویژگی‌ها به‌عنوان **پوشه‌های ایزوله** با یک `index.ts` برای صادرات بشکه‌ای.
- اجتناب از صادرات پیش‌فرض در کتابخانه‌های مشترک برای **کمک به تحلیل استاتیک**.

<br />

### 12. درک شما از حوزه و بالابری (hoisting) در جاوااسکریپت چیست و چگونه از مشکلات رایج در React جلوگیری می‌کنید؟

**پاسخ:**

- **حوزه**: لغوی—در زمان نوشتن تعیین می‌شود.
- **بالابری**: `var`، اعلان‌های تابع بالابری می‌شوند.

در React:

- استفاده از `let`/`const` برای جلوگیری از باگ‌های بالابری.
- اجتناب از تکیه بر متغیرهای بالابری‌شده در کلوژرها یا هوک‌ها.
- نگه داشتن اعلان‌های متغیر **درون حوزه هوک/کامپوننت**.

<br />

### 13. چگونه یک کتابخانه ابزار جاوااسکریپت برای یک تیم React طراحی می‌کنید که تعادل بین محصورسازی و قابلیت استفاده مجدد را حفظ کند؟

**پاسخ:**

- استفاده از **توابع خالص**.
- سازمان‌دهی بر اساس **دامنه** (مثل `formatters/`، `validators/`).
- نوشتن **تایپ‌های TypeScript و JSDoc** واضح.
- اجتناب از وضعیت داخلی یا افکت‌های جانبی.
- ارائه **پیکربندی‌های پیش‌فرض** اما امکان بازنویسی.

<br />

### 14. چگونه اصول برنامه‌نویسی تابعی (مثل تغییرناپذیری، توابع خالص) را در یک برنامه React اعمال می‌کنید؟

- استفاده از `map`، `filter` و `reduce` برای تبدیل داده‌ها.
- اجتناب از تغییر وضعیت (مثل عملگرهای گسترش).
- استخراج **کمکی‌های خالص** برای سلکتورها و منطق تجاری.
- کتابخانه‌ها: Lodash/fp، Ramda (در صورت نیاز).

<br />

### 15. رویکرد شما برای مموایز کردن محاسبات سنگین در جاوااسکریپت برای یک برنامه React چیست؟

استفاده از `useMemo`:

```jsx
const filtered = useMemo(() => heavyFilter(data), [data]);
```

از بهینه‌سازی زودهنگام اجتناب کنید؛ ابتدا پروفایل کنید. اطمینان حاصل کنید که وابستگی‌ها درست هستند تا از مقادیر قدیمی یا بازمحاسبه جلوگیری شود.

<br />

### 16. چگونه عملکرد جاوااسکریپت را در یک برنامه React با به حداقل رساندن تغییرات شیء بهینه می‌کنید؟

- استفاده از **به‌روزرسانی‌های تغییرناپذیر** (مثل عملگرهای گسترش، `immer`).
- اجتناب از مرتب‌سازی درجا یا افزودن به آرایه‌ها.
- به React کمک می‌کند تغییرات را از طریق **مقایسه سطحی** تشخیص دهد (`React.memo`، `PureComponent`).

<br />

### 17. چگونه از پروکسی‌ها یا Reflect جاوااسکریپت در یک برنامه React برای مدیریت وضعیت پویا یا اشکال‌زدایی استفاده می‌کنید؟

استفاده از `Proxy` برای ردیابی تغییرات یا ساخت بسته‌بندی‌های شبه‌ری‌اکتیو:

```jsx
const state = new Proxy(
  {},
  {
    set(target, key, value) {
      console.log(`${key} changed to ${value}`);
      target[key] = value;
      return true;
    },
  }
);
```

مناسب برای **اشکال‌زدایی**، **کتابخانه‌های فرم** یا **مشاهده‌پذیرهای سفارشی**.

<br />

### 18. درک شما از جمع‌آوری زباله جاوااسکریپت چیست و چگونه از نشت حافظه در یک برنامه React جلوگیری می‌کنید؟

جاوااسکریپت از **جمع‌آوری زباله علامت‌گذاری و جاروب** استفاده می‌کند. نشت‌های حافظه زمانی رخ می‌دهند که اشیاء به‌طور ناخواسته ارجاع می‌مانند.

در React:

- **پاکسازی** در `useEffect`.
- اجتناب از ارجاعات قدیمی یا نگه داشتن گره‌های DOM در کلوژرها.
- نظارت بر نشت‌ها با استفاده از تب Memory در Chrome DevTools.

<br />

### 19. چگونه مشکلات دقت اعداد اعشاری جاوااسکریپت را در یک برنامه React مدیریت می‌کنید (مثل محاسبات مالی)؟

از اعداد اعشاری بومی برای پول اجتناب کنید. استفاده از:

- **`Intl.NumberFormat`** برای نمایش.
- **Big.js**، **decimal.js** یا `BigInt` برای محاسبات.

<br />

### 20. رویکرد شما برای پلی‌فیل یا شیم کردن ویژگی‌های مدرن جاوااسکریپت برای مرورگرهای قدیمی در یک برنامه React چیست؟

- استفاده از **Babel + core-js** برای تراپایل/پلی‌فیل‌ها.
- استفاده از پیکربندی **browserslist** برای هدف‌گذاری مرورگرهای پشتیبانی‌شده.
- برای ویژگی‌های بحرانی (مثل `fetch`، `Promise`)، از پلی‌فیل‌های شرطی یا واردات دینامیک استفاده کنید.