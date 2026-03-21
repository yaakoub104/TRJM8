<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TRJM8 V Final</title>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Arial}

body{
background:#000;
color:#fff;
display:flex;
justify-content:center;
align-items:center;
min-height:100vh;
}

.container{
width:100%;
max-width:700px;
padding:30px 20px;
}

h1{
text-align:center;
font-size:45px;
letter-spacing:4px;
margin-bottom:10px;
}

.subtitle{
text-align:center;
color:#aaa;
margin-bottom:25px;
}

textarea{
width:100%;
height:140px;
border-radius:14px;
border:none;
padding:15px;
font-size:16px;
margin-bottom:15px;
}

.lang-box{
display:flex;
gap:10px;
margin-bottom:15px;
}

select{
flex:1;
padding:12px;
border-radius:12px;
border:none;
font-size:15px;
}

button{
width:100%;
padding:14px;
border-radius:14px;
border:none;
background:#fff;
color:#000;
font-size:17px;
cursor:pointer;
font-weight:bold;
margin-top:10px;
}

.result{
margin-top:25px;
background:#111;
padding:20px;
border-radius:14px;
min-height:80px;
line-height:1.7;
}

.ad{
margin-top:20px;
background:#111;
padding:12px;
border-radius:12px;
text-align:center;
color:#aaa;
}

.history{
margin-top:20px;
background:#111;
padding:15px;
border-radius:14px;
font-size:14px;
max-height:150px;
overflow:auto;
}
</style>
</head>

<body>

<div class="container">

<h1>TRJM8</h1>
<div class="subtitle">ترجمة فورية + إيموجي ذكي</div>

<textarea id="text" placeholder="اكتب النص هنا..."></textarea>

<div class="lang-box">
<select id="fromLang">
<option value="auto">كشف تلقائي</option>
<option value="ar">العربية</option>
<option value="en">English</option>
<option value="fr">Français</option>
<option value="es">Español</option>
<option value="de">Deutsch</option>
<option value="it">Italiano</option>
<option value="tr">Türkçe</option>
<option value="ru">Русский</option>
<option value="pt">Português</option>
<option value="ja">Japanese</option>
<option value="ko">Korean</option>
</select>

<select id="toLang">
<option value="en">English</option>
<option value="ar">العربية</option>
<option value="fr">Français</option>
<option value="es">Español</option>
<option value="de">Deutsch</option>
<option value="it">Italiano</option>
<option value="tr">Türkçe</option>
<option value="ru">Русский</option>
<option value="pt">Português</option>
<option value="ja">Japanese</option>
<option value="ko">Korean</option>
</select>
</div>

<button onclick="showAd()">ترجمة الآن</button>

<div class="result" id="result">
النتيجة تظهر هنا
</div>

<div class="ad">
اعلان Google AdSense هنا
</div>

<div class="history" id="history">
سجل الترجمات
</div>

</div>

<script>

function showAd(){
document.getElementById("result").innerText="جاري عرض الإعلان...";
setTimeout(function(){
translateText();
},3000);
}

function translateText(){

let text=document.getElementById("text").value;
let from=document.getElementById("fromLang").value;
let to=document.getElementById("toLang").value;

let url=`https://translate.googleapis.com/translate_a/single?client=gtx&sl=${from}&tl=${to}&dt=t&q=${encodeURIComponent(text)}`;

fetch(url)
.then(res=>res.json())
.then(data=>{

let result=data[0][0][0];

let emoji="";

if(result.includes("love")) emoji=" ❤️";
else if(result.includes("happy")) emoji=" 😊";
else if(result.includes("food")) emoji=" 🍔";
else if(result.includes("car")) emoji=" 🚗";
else if(result.includes("money")) emoji=" 💰";
else if(result.includes("hello")) emoji=" 👋";
else emoji=" 🌍";

document.getElementById("result").innerText=result + emoji;

let history=document.getElementById("history");
history.innerHTML+="<br>"+result + emoji;

});
}

</script>

</body>
</html>
