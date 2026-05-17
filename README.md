<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="老K預測">
<meta name="theme-color" content="#050505">

<title>老K百家預測程式</title>dth=device-width, initial-scale=1.0">
<title>老K百家預測程式</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;}
body{
    background:#050505;
    display:flex;
    justify-content:center;
    align-items:center;
    min-height:100vh;
    font-family:"Microsoft JhengHei",sans-serif;
    overflow:hidden;
}
.phone{
    width:430px;
    height:932px;
    position:relative;
    overflow:hidden;
    border-radius:40px;
    background:
        radial-gradient(circle at 50% 10%, rgba(255,215,120,.10), transparent 16%),
        radial-gradient(circle at 50% 48%, rgba(212,175,55,.035), transparent 32%),
        linear-gradient(180deg,#15100b 0%, #090807 38%, #020202 100%);
}
.phone::before{
    content:"";
    position:absolute;
    inset:0;
    background:
        linear-gradient(rgba(212,175,55,.012) 1px, transparent 1px),
        linear-gradient(90deg, rgba(212,175,55,.012) 1px, transparent 1px);
    background-size:28px 28px;
}
.phone::after{
    content:"";
    position:absolute;
    top:-120%;
    left:0;
    width:100%;
    height:240%;
    background:linear-gradient(180deg,transparent 0%,rgba(255,215,120,.04) 50%,transparent 100%);
    animation:scanMove 7s linear infinite;
}
@keyframes scanMove{
    from{transform:translateY(-30%)}
    to{transform:translateY(30%)}
}
.hud-frame{
    position:absolute;
    inset:18px;
    border:1px solid rgba(212,175,55,.06);
    border-radius:28px;
}
.hud-frame::before,.hud-frame::after{
    content:"";
    position:absolute;
    width:52px;
    height:52px;
    border:2px solid rgba(212,175,55,.14);
}
.hud-frame::before{
    top:-2px;
    left:-2px;
    border-right:none;
    border-bottom:none;
}
.hud-frame::after{
    bottom:-2px;
    right:-2px;
    border-left:none;
    border-top:none;
}
.particle{
    position:absolute;
    width:8px;
    height:8px;
    border-radius:50%;
    background:rgba(255,220,140,0.6);
    box-shadow:0 0 14px rgba(255,220,140,0.25);
    animation:particlePulse 3s infinite ease-in-out;
    z-index:5;
}
.p1{top:310px;left:78px;}
.p2{top:430px;right:70px;animation-delay:1s;}
.p3{bottom:260px;left:95px;animation-delay:1.8s;}
@keyframes particlePulse{
    0%,100%{transform:scale(1);opacity:.2;}
    50%{transform:scale(1.8);opacity:.9;}
}
.title-box{
    position:absolute;
    top:28px;
    left:50%;
    transform:translateX(-50%);
    width:390px;
    height:78px;
    border:1px solid rgba(176,138,60,.24);
    border-radius:18px;
    background:linear-gradient(180deg,rgba(38,26,10,.94),rgba(12,8,3,.84));
    display:flex;
    justify-content:center;
    align-items:center;
    z-index:50;
    overflow:hidden;
}
.title-box::before{
    content:"";
    position:absolute;
    top:-60px;
    left:-220px;
    width:140px;
    height:240px;
    background:linear-gradient(90deg,transparent,rgba(255,255,255,.35),transparent);
    transform:rotate(24deg);
    filter:blur(2px);
    animation:shine 5s infinite;
}
@keyframes shine{
    0%{left:-220px;opacity:0}
    15%{opacity:1}
    45%{left:460px;opacity:1}
    60%{opacity:0}
    100%{left:460px;opacity:0}
}
.title{
    font-size:34px;
    font-weight:900;
    letter-spacing:3px;
    color:#c8962f;
}
.page{
    position:absolute;
    inset:0;
    z-index:30;
    display:flex;
    justify-content:center;
    align-items:center;
}
.center-box{
    width:320px;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    text-align:center;
    transform:translateY(30px);
}
.input-label{
    color:#d9b86d;
    font-size:18px;
    font-weight:900;
    margin-bottom:12px;
}
.input-box,select{
    width:100%;
    height:58px;
    border-radius:16px;
    border:1px solid rgba(212,175,55,.30);
    background:rgba(20,14,8,.92);
    color:#f0c96d;
    font-size:22px;
    text-align:center;
    outline:none;
    margin-bottom:16px;
}
select{font-size:18px;}
.btn,.action-btn,.predict-btn{
    width:100%;
    height:64px;
    border:1px solid rgba(212,175,55,.20);
    border-radius:18px;
    background:linear-gradient(180deg,rgba(40,28,10,.76),rgba(12,8,3,.54));
    color:#f0c96d;
    font-size:24px;
    font-weight:800;
    cursor:pointer;
    margin-bottom:16px;
    transition:all .22s ease;
    box-shadow:0 0 0 rgba(212,175,55,0), inset 0 1px 0 rgba(255,255,255,.06);
}
.btn:hover,.action-btn:hover,.predict-btn:hover{
    transform:translateY(-3px);
    border-color:rgba(255,215,120,.45);
    box-shadow:0 0 18px rgba(212,175,55,.16),0 8px 20px rgba(0,0,0,.28);
}
.btn:active,.action-btn:active,.predict-btn:active{
    transform:scale(.96);
}
.action-row{
    display:flex;
    gap:10px;
    width:100%;
}
.action-btn{
    flex:1;
    height:56px;
    font-size:18px;
}
.hidden{display:none!important;}
.result-page{
    position:absolute;
    inset:0;
    display:none;
    z-index:1200;
}
.result-content{
    position:absolute;
    top:150px;
    left:50%;
    transform:translateX(-50%);
    width:390px;
}
.card{
    width:100%;
    background:rgba(20,14,8,.78);
    border:1px solid rgba(212,175,55,.22);
    border-radius:18px;
    padding:20px;
    backdrop-filter:blur(10px);
    margin-bottom:18px;
}
.card-title{
    color:#ffd98a;
    font-size:14px;
    font-weight:900;
    margin-bottom:14px;
}
.table-main{
    color:#fff;
    font-size:22px;
    font-weight:900;
}
.table-id{
    color:#ffd98a;
    font-size:32px;
    font-weight:900;
    margin:18px 0;
}
.status-live{
    display:flex;
    align-items:center;
    gap:8px;
    color:#53ff76;
    font-size:14px;
    font-weight:800;
}
.dot{
    width:10px;
    height:10px;
    border-radius:50%;
    background:#53ff76;
    box-shadow:0 0 10px #53ff76;
}
.version{
    color:#d9b86d;
    font-size:13px;
    margin-top:10px;
}
.predict-row{
    font-size:20px;
    font-weight:900;
    margin:12px 0;
}
.predict-red{
    color:#ff5b5b;
    text-shadow:0 0 12px rgba(255,80,80,.7);
}
.predict-blue{
    color:#57a6ff;
    text-shadow:0 0 12px rgba(87,166,255,.7);
}
.predict-gold{
    font-size:20px;
    font-weight:900;
    margin:12px 0;
    color:#ffd98a;
}
.quick-loader,.boot-loader{
    position:absolute;
    inset:0;
    display:none;
    justify-content:center;
    align-items:center;
    flex-direction:column;
    z-index:3000;
    background:rgba(0,0,0,.35);
    backdrop-filter:blur(3px);
}
.loader-ring{
    width:72px;
    height:72px;
    border-radius:50%;
    border:3px solid rgba(212,175,55,.15);
    border-top:3px solid #ffd98a;
    animation:quickSpin .5s linear infinite;
    box-shadow:0 0 20px rgba(255,215,138,.2);
}
.loader-text{
    margin-top:18px;
    color:#ffd98a;
    font-size:18px;
    font-weight:900;
    letter-spacing:2px;
    text-align:center;
}
@keyframes quickSpin{
    from{transform:rotate(0deg);}
    to{transform:rotate(360deg);}
}
</style>
</head>
<body>
<div class="phone">
<div class="hud-frame"></div>
<div class="particle p1"></div>
<div class="particle p2"></div>
<div class="particle p3"></div>

<div class="title-box"><div class="title">老K百家預測程式</div></div>

<div class="page" id="page1">
<div class="center-box">
<div class="input-label">請輸入局號</div>
<input class="input-box" id="roundInput" type="text" value="12802-37">
<button class="btn" onclick="goPage2()">下一步</button>
</div>
</div>

<div class="page hidden" id="page2">
<div class="center-box">
<button class="btn" onclick="showMT()">MT真人</button>
<button class="btn">DG真人</button>
</div>
</div>

<div class="page hidden" id="page3">
<div class="center-box">
<div class="input-label">起始本金</div>
<input class="input-box" id="capitalInput" type="number">
<select id="roomSelect">
<option value="" selected="" disabled="">請選擇牌桌</option>
<option>百家樂1</option>
<option>百家樂2</option>
<option>百家樂3</option>
<option>百家樂3A</option>
<option>百家樂5</option>
<option>百家樂6</option>
<option>百家樂7</option>
<option>百家樂8</option>
<option>百家樂9</option>
<option>百家樂10</option>
<option>百家樂11</option>
<option>百家樂12</option>
<option>百家樂13</option>
<option>百家樂13A</option>
<option>百家樂15</option>
<option>百家樂16</option>
</select>
<div class="action-row">
<button class="action-btn" onclick="goBack()">上一步</button>
<button class="action-btn" onclick="bootSystem()">系統啟動</button>
</div>
</div>
</div>

<div class="result-page" id="resultPage">
<div class="title-box"><div class="title">老K百家預測程式</div></div>
<div class="result-content">
<div class="card">
<div class="card-title">牌桌資訊</div>
<div class="table-main" id="resultRoom"></div>
<div class="table-id" id="roundText"></div>
<div class="status-live"><div class="dot"></div>系統連線狀態：正常</div>
<div class="version">版本號：V5.2.8</div>
</div>

<div class="card hidden" id="predictCard">
<div class="card-title">預測結果</div>
<div class="predict-row" id="predictText"></div>
<div class="predict-gold" id="confidenceText"></div>
<div class="predict-gold" id="betText"></div>
</div>

<button class="predict-btn" onclick="startPredict()">開始預測</button>
</div>
</div>

<div class="quick-loader" id="quickLoader">
<div class="loader-ring"></div>
<div class="loader-text">系統分析中...</div>
</div>

<div class="boot-loader" id="bootLoader">
<div class="loader-ring"></div>
<div class="loader-text" id="bootText">系統啟動中...</div>
</div>
</div>

<script>
let roundBase = "";
let roundNumber = 0;

const bootMessages = [
"系統啟動中...",
"驗證授權憑證...",
"建立安全連線...",
"連線資料庫...",
"同步牌桌訊號...",
"載入預測核心...",
"初始化分析模組...",
"校正演算法參數...",
"建立機率模型...",
"啟動決策引擎...",
"系統啟動完成"
];

function parseRoundInput(){
    const val = roundInput.value.trim() || "12802-37";
    if(val.includes("-")){
        const parts = val.split("-");
        roundBase = parts[0];
        roundNumber = parseInt(parts[1]) || 0;
    }else{
        roundBase = val;
        roundNumber = 0;
    }
}
function getRoundDisplay(){
    return roundNumber > 0 ? `${roundBase}-${roundNumber}` : roundBase;
}
function goPage2(){
    page1.classList.add('hidden');
    page2.classList.remove('hidden');
}
function showMT(){
    page2.classList.add('hidden');
    page3.classList.remove('hidden');
}
function goBack(){
    page3.classList.add('hidden');
    page2.classList.remove('hidden');
}
function calcBet(capital, confidence){
    let percent = 0.05;
    if(confidence >= 67 && confidence <= 69) percent = 0.06;
    else if(confidence >= 70 && confidence <= 72) percent = 0.07;
    else if(confidence >= 73 && confidence <= 75) percent = 0.08;
    else if(confidence >= 76 && confidence <= 77) percent = 0.09;
    else if(confidence >= 78) percent = 0.10;
    return Math.floor((capital * percent) / 100) * 100;
}
function bootSystem(){
    parseRoundInput();
    bootLoader.style.display='flex';
    let i = 0;
    const timer = setInterval(()=>{
        bootText.innerText = bootMessages[i];
        i++;
        if(i >= bootMessages.length){
            clearInterval(timer);
            setTimeout(()=>{
                bootLoader.style.display='none';
                enterResult();
            },300);
        }
    },270);
}
function flashAnalyze(callback){
    quickLoader.style.display='flex';
    setTimeout(()=>{
        quickLoader.style.display='none';
        callback();
    },500);
}
function enterResult(){
    resultRoom.innerText = roomSelect.value;
    roundText.innerText = getRoundDisplay();
    page3.classList.add('hidden');
    resultPage.style.display='block';
}
function startPredict(){
    roundNumber++;
    flashAnalyze(()=>{
        const capital = parseInt(capitalInput.value || 10000);
        const confidence = Math.floor(Math.random() * 16) + 64;
        const isBanker = Math.random() < 0.5;
        const bet = calcBet(capital, confidence);

        roundText.innerText = getRoundDisplay();
        confidenceText.innerText = "信心指數：" + confidence + "%";
        betText.innerText = "建議配注：" + bet;
        predictText.className = "predict-row " + (isBanker ? "predict-red" : "predict-blue");
        predictText.innerText = "推薦：" + (isBanker ? "莊" : "閒");
        predictCard.classList.remove('hidden');
    });
}
</script>

</body></html>
