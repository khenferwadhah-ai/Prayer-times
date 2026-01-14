<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ø£ÙˆÙ‚Ø§Øª Ø§Ù„ØµÙ„Ø§Ø© - Ø¬Ù…Ø¹ÙŠØ© Ù…Ø³Ùƒ Ø§Ù„Ø®ØªØ§Ù…</title>
<style>
body {
font-family: "Arial", sans-serif;
background-color: #f0f5f0;
color: #064e3b;
display: flex;
justify-content: center;
align-items: center;
height: 100vh;
margin: 0;
direction: rtl;
}
.container {
background-color: #e6f2e6;
padding: 30px 40px;
border-radius: 20px;
box-shadow: 0 5px 15px rgba(0,0,0,0.2);
text-align: center;
width: 320px;
}
h1 {
color: #047857;
margin-bottom: 20px;
}
ul {
list-style: none;
padding: 0;
margin: 0;
}
li {
font-size: 18px;
margin: 8px 0;
padding: 5px 0;
border-bottom: 1px solid #a7f3d0;
}
.footer {
margin-top: 15px;
font-size: 12px;
color: #065f46;
}
</style>
</head>
<body>
<div class="container">
<h1>Ø£ÙˆÙ‚Ø§Øª Ø§Ù„ØµÙ„Ø§Ø© Ø§Ù„ÙŠÙˆÙ…</h1>
<ul id="prayer-times">
<li>ØªØ­Ù…ÙŠÙ„ Ø§Ù„Ø£ÙˆÙ‚Ø§Øª...</li>
</ul>
<div class="footer">Ø§Ù„Ø¬Ù…Ø¹ÙŠØ© Ø§Ù„Ø®ÙŠØ±ÙŠØ© Ù…Ø³Ùƒ Ø§Ù„Ø®ØªØ§Ù… - Ø§Ù„Ù‚Ø±Ø§Ø±Ù… Ù‚ÙˆÙ‚Ø©</div>
</div>

<script>
// Ø§Ø³ØªØ¨Ø¯Ù„ city Ùˆ country Ø¨Ø§Ø³Ù… Ù…Ø¯ÙŠÙ†ØªÙƒ
const city = "ElQararm";
const country = "Algeria";
const method = 4; // Ø·Ø±ÙŠÙ‚Ø© Ø§Ù„Ø­Ø³Ø§Ø¨ Ø§Ù„Ù…Ø­Ù„ÙŠØ©

async function fetchPrayerTimes() {
try {
const response = await fetch(`https://api.aladhan.com/v1/timingsByCity?city=${city}&country=${country}&method=${method}`);
const data = await response.json();
const times = data.data.timings;
let html = "";
for (const prayer in times) {
html += `<li>${prayer}: ${times[prayer]}</li>`;
}
document.getElementById("prayer-times").innerHTML = html;
} catch (error) {
document.getElementById("prayer-times").innerHTML = "<li>ØªØ¹Ø°Ø± ØªØ­Ù…ÙŠÙ„ Ø§Ù„Ø£ÙˆÙ‚Ø§Øª</li>";
console.error(error);
}
}

// ØªØ­Ø¯ÙŠØ« Ø§Ù„Ø£ÙˆÙ‚Ø§Øª Ø¹Ù†Ø¯ ÙØªØ­ Ø§Ù„ØµÙØ­Ø©
fetchPrayerTimes();
</script>
</body>
</html>
