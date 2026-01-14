<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>الجمعية الخيرية مسك الختام - أوقات الصلاة</title>

  <!-- صورة عند مشاركة الرابط على فيسبوك -->
  <meta property="og:title" content="الجمعية الخيرية مسك الختام - أوقات الصلاة">
  <meta property="og:description" content="أوقات الصلاة اليومية للڨرارم – ولاية ميلة.">
  <meta property="og:image" content="https://raw.githubusercontent.com/khen1/khenferwadhah-ai/main/prayer.jpg">
  <meta property="og:type" content="website">

  <style>
    body {
      font-family: "Arial", sans-serif;
      background-color: #f0f5f0;
      color: #064e3b;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }
    .container {
      background-color: #e6f2e6;
      padding: 30px 40px;
      border-radius: 20px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.2);
      text-align: center;
      width: 360px;
    }
    h1 {
      color: #047857;
      margin-bottom: 15px;
      font-size: 22px;
    }
    ul {
      list-style: none;
      padding: 0;
      margin: 0 0 20px 0;
    }
    li {
      font-size: 18px;
      margin: 6px 0;
    }
    .date-time {
      margin-bottom: 15px;
      font-size: 16px;
    }
    footer {
      font-size: 14px;
      color: #065f46;
    }
  </style>
</head>
<body>

<div class="container">
  <h1>الجمعية الخيرية مسك الختام</h1>

  <!-- التاريخ والوقت -->
  <div class="date-time">
    <div id="gregorian"></div>
    <div id="hijri"></div>
    <div id="clock"></div>
  </div>

  <!-- أوقات الصلاة -->
  <ul>
    <li>الفجر: <span id="fajr"></span></li>
    <li>الشروق: <span id="sunrise"></span></li>
    <li>الظهر: <span id="dhuhr"></span></li>
    <li>العصر: <span id="asr"></span></li>
    <li>المغرب: <span id="maghrib"></span></li>
    <li>العشاء: <span id="isha"></span></li>
  </ul>

  <footer>جميع الحقوق محفوظة © الجمعية الخيرية مسك الختام</footer>
</div>

<script>
  // ========================
  // الساعة الرقمية والتاريخ
  // ========================
  function updateClock() {
    const now = new Date();

    // التاريخ الميلادي
    const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
    document.getElementById("gregorian").innerText = "التاريخ الميلادي: " + now.toLocaleDateString('ar-DZ', options);

    // الساعة
    const hours = String(now.getHours()).padStart(2,'0');
    const minutes = String(now.getMinutes()).padStart(2,'0');
    const seconds = String(now.getSeconds()).padStart(2,'0');
    document.getElementById("clock").innerText = "الساعة: " + hours + ":" + minutes + ":" + seconds;

    // التاريخ الهجري
    fetch("https://api.aladhan.com/v1/gToH?date=" + now.getFullYear() + "-" + (now.getMonth()+1) + "-" + now.getDate())
      .then(res => res.json())
      .then(data => {
        document.getElementById("hijri").innerText = "التاريخ الهجري: " + data.data.hijri.date;
      });
  }
  setInterval(updateClock, 1000);
  updateClock();

  // ========================
  // أوقات الصلاة للڨرارم ولاية ميلة
  // ========================
  fetch("https://api.aladhan.com/v1/timings?latitude=36.276&longitude=6.162&method=3&timezonestring=Africa/Algiers")
    .then(response => response.json())
    .then(data => {
      const t = data.data.timings;
      document.getElementById("fajr").innerText = t.Fajr;
      document.getElementById("sunrise").innerText = t.Sunrise;
      document.getElementById("dhuhr").innerText = t.Dhuhr;
      document.getElementById("asr").innerText = t.Asr;
      document.getElementById("maghrib").innerText = t.Maghrib;
      document.getElementById("isha").innerText = t.Isha;
    });
</script>

</body>
</html>
