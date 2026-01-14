<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>مواقيت الصلاة - بلدية القرارم قوقة</title>
<style>
body{
    font-family: Arial;
    text-align: center;
    background: linear-gradient(#0b4d2b,#0e7a3c);
    color: white;
}
.card{
    background:white;
    color:black;
    margin:20px auto;
    padding:20px;
    width:320px;
    border-radius:20px;
}
</style>
</head>

<body>

<h2>🕌 مواقيت الصلاة – بلدية القرارم قوقة</h2>
<h3 id="date"></h3>
<h1 id="clock"></h1>

<div class="card">
<p>الفجر: <span id="fajr"></span></p>
<p>الظهر: <span id="dhuhr"></span></p>
<p>العصر: <span id="asr"></span></p>
<p>المغرب: <span id="maghrib"></span></p>
<p>العشاء: <span id="isha"></span></p>
</div>

<script>
setInterval(()=>{
    let now = new Date();
    document.getElementById("clock").innerHTML = now.toLocaleTimeString();
    document.getElementById("date").innerHTML = now.toLocaleDateString();
},1000);

fetch("https://api.aladhan.com/v1/timingsByCity?city=Mila&country=Algeria&method=2")
.then(r=>r.json())
.then(d=>{
 let t=d.data.timings;
 document.getElementById("fajr").innerHTML=t.Fajr;
 document.getElementById("dhuhr").innerHTML=t.Dhuhr;
 document.getElementById("asr").innerHTML=t.Asr;
 document.getElementById("maghrib").innerHTML=t.Maghrib;
 document.getElementById("isha").innerHTML=t.Isha;
});
</script>

</body>
</html>
