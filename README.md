<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title id="pageTitle">Dollar Exchange - User Panel</title>
<link id="favicon" rel="icon" href="">
<link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{--primary:#0b75ff;--secondary:#0037dd;--bg:#f1f5f9;--card:#ffffff;--text:#0f172a;--muted:#64748b;--border:#e2e8f0;--radius:16px}
*{box-sizing:border-box}
body{font-family:'Hind Siliguri',sans-serif;background:var(--bg);margin:0;color:var(--text);min-height:100vh}

#loadingScreen{position:fixed;top:0;left:0;right:0;bottom:0;background:#fff;display:flex;justify-content:center;align-items:center;flex-direction:column;z-index:99999;transition:opacity .5s ease}
.loader{width:52px;height:52px;border:5px solid #e2e8f0;border-top:5px solid var(--primary);border-radius:50%;animation:spin 1s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.loading-text{margin-top:15px;color:var(--primary);font-weight:700}

.typing-text{display:inline-block;border-right:2px solid #fff;padding-right:5px;animation:blink-caret .75s step-end infinite}
@keyframes blink-caret{from,to{border-color:transparent}50%{border-color:#fff}}

.topbar{background:#fff;padding:12px 16px;display:flex;align-items:center;justify-content:space-between;gap:10px;box-shadow:0 2px 10px rgba(15,23,42,.06);flex-wrap:wrap}
.logo{display:flex;align-items:center;gap:10px}
.logo img{width:46px;height:46px;border-radius:12px;object-fit:cover;box-shadow:0 2px 8px rgba(0,0,0,.08)}
#siteName{font-size:16px;font-weight:700;color:var(--secondary)}
.status-badge{padding:6px 14px;border-radius:20px;color:#fff;font-size:13px;font-weight:700;display:inline-block}
.offline{background:#ef4444}
.online{background:#22c55e}
.top-buttons{display:flex;gap:8px;align-items:center}
.top-buttons button{padding:8px 16px;border-radius:22px;border:1.5px solid var(--primary);background:#fff;color:var(--primary);font-weight:700;cursor:pointer;transition:.2s;font-family:inherit}
.top-buttons button:hover{background:var(--primary);color:#fff}

.blue-head{background:linear-gradient(135deg,var(--secondary),var(--primary));padding:34px 18px;text-align:center;border-bottom-left-radius:26px;border-bottom-right-radius:26px;color:#fff;box-shadow:0 8px 24px rgba(0,55,221,.25)}
.blue-head h1{margin:0;font-size:26px;letter-spacing:.2px;font-weight:700}
.blue-head p{margin:8px 0 0;opacity:.92}

.card{width:92%;max-width:720px;margin:16px auto;background:var(--card);padding:18px;border-radius:var(--radius);box-shadow:0 4px 16px rgba(15,23,42,.06);border:1px solid var(--border)}
.card-title{font-size:17px;font-weight:700;margin:0 0 12px;display:flex;align-items:center;gap:8px}

label{display:block;font-size:13.5px;font-weight:600;color:#334155;margin:12px 0 4px}
input,select,textarea{width:100%;padding:12px 14px;margin:0;border-radius:10px;border:1.5px solid var(--border);font-size:15px;box-sizing:border-box;background:#f8fafc;transition:.2s;font-family:inherit}
input:focus,select:focus,textarea:focus{outline:none;border-color:var(--primary);background:#fff;box-shadow:0 0 0 3px rgba(11,117,255,.12)}
button.primary{background:linear-gradient(135deg,var(--primary),var(--secondary));color:#fff;border:none;padding:13px;border-radius:10px;cursor:pointer;font-weight:700;font-size:16px;margin-top:16px;transition:.2s;box-shadow:0 4px 12px rgba(11,117,255,.3);font-family:inherit}
button.primary:hover{transform:translateY(-1px);box-shadow:0 6px 16px rgba(11,117,255,.4)}
button.danger{background:#ef4444;color:#fff;border:none;padding:11px;border-radius:8px;cursor:pointer}
button.success{background:#16a34a;color:#fff;border:none;padding:11px;border-radius:8px;cursor:pointer}

.trade-type-toggle{display:flex;background:#eef2f7;border-radius:12px;overflow:hidden;margin:14px 0 4px;padding:4px;gap:4px}
.trade-type-toggle button{flex:1;padding:11px;border:none;background:transparent;cursor:pointer;font-weight:700;border-radius:9px;transition:.25s;color:#475569;font-size:15px;font-family:inherit}
.trade-type-toggle button.active{background:linear-gradient(135deg,var(--primary),var(--secondary));color:#fff;box-shadow:0 3px 8px rgba(11,117,255,.35)}

.pay-info{background:#eff6ff;border:1.5px dashed #93c5fd;border-radius:12px;padding:12px 14px;margin-top:14px;animation:fadeIn .3s ease}
@keyframes fadeIn{from{opacity:0;transform:translateY(-4px)}to{opacity:1;transform:none}}
.pay-info .pay-label{font-size:13.5px;font-weight:700;color:#1e40af;margin-bottom:6px}
.pay-id-row{display:flex;align-items:center;justify-content:space-between;gap:10px;background:#fff;border-radius:8px;padding:9px 12px;border:1px solid #dbeafe}
.pay-id-row b{overflow-wrap:anywhere;font-size:15px}

.fee-box{background:#fffbeb;border:1px solid #fde68a;border-radius:10px;padding:10px 14px;margin:12px 0;font-size:13.5px;color:#92400e}

.order-box{background:#f8fafc;margin:10px 0;border-radius:12px;padding:13px;border:1px solid var(--border);display:flex;justify-content:space-between;align-items:center;gap:10px;transition:.2s}
.order-box:hover{border-color:#bfdbfe;box-shadow:0 2px 10px rgba(11,117,255,.08)}
.order-info{flex:1;min-width:0}
.order-meta{min-width:110px;text-align:right}
.status{padding:5px 12px;border-radius:20px;color:#fff;font-weight:700;font-size:12.5px;display:inline-block}
.pending{background:#f59e0b}
.completed{background:#16a34a}
.rejected{background:#ef4444}

#nav{display:flex;justify-content:center;gap:8px;background:#0f172a;padding:12px 14px;flex-wrap:wrap}
#nav button{width:auto;flex:1 1 auto;min-width:120px;max-width:260px;background:#16a34a;color:#fff;border:none;padding:11px 14px;border-radius:10px;font-weight:700;cursor:pointer;font-family:inherit;font-size:14.5px;transition:.2s}
#nav button:hover{filter:brightness(1.1)}
#nav button.menu-btn{background:linear-gradient(135deg,var(--primary),var(--secondary))}

.wa-btn{position:fixed;bottom:22px;left:18px;background:#25d366;width:60px;height:60px;border-radius:50%;display:flex;justify-content:center;align-items:center;box-shadow:0 6px 16px rgba(0,0,0,.2);z-index:90;transition:.2s}
.wa-btn:hover{transform:scale(1.06)}
.wa-btn img{width:32px;height:32px;border-radius:50%;object-fit:cover}
.small{font-size:13px;color:var(--muted)}
.modal{position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(15,23,42,.55);display:flex;justify-content:center;align-items:center;padding:20px;z-index:1000;overflow:auto;backdrop-filter:blur(3px)}
.modal .box{width:100%;max-width:520px;background:#fff;border-radius:16px;padding:20px;margin:auto;max-height:90vh;overflow-y:auto;box-shadow:0 20px 50px rgba(0,0,0,.25)}
.modal .box h3{margin-top:0}
.id-badge{background:#f8fafc;padding:9px 12px;border-radius:10px;display:inline-block;width:100%;margin-bottom:7px;border:1px solid var(--border)}
.order-empty{text-align:center;color:var(--muted);padding:26px}
.account-info{display:flex;gap:10px;align-items:center}
.btn-ghost{background:transparent;border:1.5px solid var(--primary);color:var(--primary);padding:9px 14px;border-radius:9px;cursor:pointer;font-weight:600;font-family:inherit}
.btn-ghost:hover{background:var(--primary);color:#fff}

.maintenance-overlay{position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(255,255,255,.97);z-index:9999;display:flex;justify-content:center;align-items:center;flex-direction:column;text-align:center;padding:20px}
.global-notification{position:fixed;top:70px;left:0;right:0;padding:11px;text-align:center;color:#fff;font-weight:700;z-index:1000;display:none;box-shadow:0 4px 12px rgba(0,0,0,.15)}
.notification-info{background-color:#31708f}
.notification-warning{background-color:#8a6d3b}
.notification-success{background-color:#5cb85c}
.notification-error{background-color:#d9534f}
body.modal-open{overflow:hidden}
.copy-btn-inside{background-color:#e2e8f0;border:none;padding:5px 12px;border-radius:6px;cursor:pointer;font-size:13px;transition:.2s;font-family:inherit;font-weight:600;width:auto}
.copy-btn-inside.copied{background-color:#16a34a;color:#fff}

/* ===== LIVE ORDERS (ট্রাস্ট ডিজাইন) ===== */
.live-badge{display:inline-flex;align-items:center;gap:8px;background:#fee2e2;color:#dc2626;padding:7px 18px;border-radius:20px;font-weight:800;font-size:14px;animation:liveGlow 2s infinite}
@keyframes liveGlow{0%{box-shadow:0 0 0 0 rgba(239,68,68,.45)}70%{box-shadow:0 0 0 14px rgba(239,68,68,0)}100%{box-shadow:0 0 0 0 rgba(239,68,68,0)}}
.live-dot{width:10px;height:10px;background:#ef4444;border-radius:50%;animation:pulse 1.2s ease-in-out infinite}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.35;transform:scale(.8)}}
.live-sub{font-size:13px;color:var(--muted);text-align:center;margin:8px 0 4px}
.trust-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin:14px 0}
.tstat{background:linear-gradient(135deg,#f0fdf4,#dcfce7);border:1px solid #bbf7d0;border-radius:12px;padding:12px 6px;text-align:center}
.tstat h4{margin:0;font-size:19px;color:#16a34a;font-weight:800}
.tstat div{font-size:12px;color:#166534;font-weight:600}
.live-order-item{display:flex;align-items:center;gap:12px;background:#f8fafc;border:1px solid var(--border);border-radius:12px;padding:11px 13px;margin:9px 0;transition:.2s}
.live-order-item:hover{border-color:#fecaca;box-shadow:0 2px 10px rgba(239,68,68,.06)}
.live-order-item.live-new{animation:flashNew 2s ease}
@keyframes flashNew{0%{background:#dcfce7;border-color:#16a34a;transform:scale(1.01)}100%{background:#f8fafc;border-color:var(--border);transform:none}}
.lo-avatar{width:40px;height:40px;min-width:40px;border-radius:50%;background:linear-gradient(135deg,var(--primary),var(--secondary));color:#fff;display:flex;justify-content:center;align-items:center;font-weight:700;font-size:16px;position:relative}
.lo-avatar.lo-done{background:linear-gradient(135deg,#16a34a,#15803d)}
.lo-verified{position:absolute;bottom:-3px;right:-3px;background:#16a34a;border:2px solid #fff;border-radius:50%;width:15px;height:15px;font-size:9px;display:flex;align-items:center;justify-content:center;color:#fff}
.lo-main{flex:1;min-width:0}
.lo-main b{font-size:14.5px}
.lo-right{text-align:right;min-width:105px}
.lo-time{font-size:12px;color:var(--muted)}

.animated-text-bar{overflow:hidden;white-space:nowrap;padding:10px 0;font-weight:700}
.animated-text-bar span{display:inline-block;white-space:nowrap;padding-left:100%;animation:scrollText 20s linear infinite}
@keyframes scrollText{0%{transform:translateX(0)}100%{transform:translateX(-100%)}}

.quote-text{font-style:italic;color:#334155;text-align:center}
.quote-author{text-align:center;color:var(--muted);margin-top:6px;font-size:13px}

footer{text-align:center;padding:24px 16px 30px;color:var(--muted);font-size:13.5px}
footer b{color:var(--secondary)}

@media (max-width:520px){
.topbar{padding:10px}
.blue-head{padding:26px 14px}
.modal .box{margin:20px;width:calc(100% - 40px)}
.lo-right{min-width:95px}
}
</style>
</head>
<body>

<div id="loadingScreen">
  <div class="loader"></div>
  <div class="loading-text">লোড হচ্ছে...</div>
</div>

<div id="globalNotification" class="global-notification"></div>

<div id="maintenanceOverlay" class="maintenance-overlay" style="display:none;">
  <h2>Site Under Maintenance</h2>
  <p id="maintenanceMessage">We are currently performing maintenance. Please check back later.</p>
</div>

<!-- Account Modal -->
<div id="accountModal" class="modal" style="display:none;">
<div class="box" onclick="event.stopPropagation()">
<h3 id="accTitle">My Account</h3>
<div id="accForms">
<div id="loginForm">
<label>Email</label><input id="loginEmail" placeholder="Email" type="email" />
<label>Password</label><input id="loginPassword" placeholder="Password" type="password" />
<button class="primary" onclick="loginUser()">Login</button>
<div style="text-align:center;margin-top:10px;display:flex;gap:8px;justify-content:center;flex-wrap:wrap">
<button class="btn-ghost" onclick="showSignup()">Sign Up</button>
<button class="btn-ghost" onclick="showFisher()">Fisher</button>
<button class="btn-ghost" onclick="showForgotPassword()">Forget Password</button>
</div>
</div>

<div id="signupForm" style="display:none">
<label>আপনার নাম</label><input id="signupName" placeholder="আপনার নাম" />
<label>Email</label><input id="signupEmail" placeholder="Email" type="email" />
<label>মোবাইল নম্বর</label><input id="signupNumber" placeholder="মোবাইল নম্বর" />
<label>Password</label><input id="signupPassword" placeholder="Password" type="password" />
<button class="primary" onclick="signupUser()">Create Account</button>
<div style="text-align:center;margin-top:10px"><button class="btn-ghost" onclick="showLogin()">Already have account</button></div>
</div>

<div id="fisherForm" style="display:none">
<label>আপনার নাম</label><input id="fisherName" placeholder="আপনার নাম" />
<label>Email</label><input id="fisherEmail" placeholder="Email" type="email" />
<label>মোবাইল নম্বর</label><input id="fisherNumber" placeholder="মোবাইল নম্বর" />
<label>Password</label><input id="fisherPassword" placeholder="Password" type="password" />
<button class="primary" onclick="signupFisher()">Create Fisher Account</button>
<div style="text-align:center;margin-top:10px"><button class="btn-ghost" onclick="showLogin()">Already have account</button></div>
</div>

<div id="forgotPasswordForm" style="display:none">
<p style="margin-bottom:10px">Enter your email address to reset your password:</p>
<label>Email</label><input id="forgotEmail" placeholder="Email" type="email" />
<button class="primary" onclick="sendPasswordReset()">Send Reset Code</button>
<div id="resetCodeSection" style="display:none;margin-top:10px">
<label>Verification Code</label><input id="resetCode" placeholder="Verification Code" />
<label>New Password</label><input id="resetNewPassword" placeholder="New Password" type="password" />
<button class="primary" onclick="resetPassword()">Reset Password</button>
</div>
<div style="text-align:center;margin-top:10px"><button class="btn-ghost" onclick="showLogin()">Back to Login</button></div>
</div>
</div>

<div id="accProfile" style="display:none">
<div style="margin-bottom:8px"><b>Logged in as:</b></div>
<div class="account-info">
<div>
<div id="pName" style="font-weight:800"></div>
<div id="pEmail" class="small"></div>
<div id="pNumber" class="small"></div>
</div>
</div>
<div style="margin-top:14px;display:flex;gap:8px">
<button class="primary" style="margin-top:0" onclick="closeAccountModal()">Close</button>
<button class="btn-ghost" onclick="logoutUser()">Logout</button>
</div>
</div>

</div>
</div>

<!-- TOP BAR -->
<div class="topbar">
<div class="logo">
<img id="logoImg" src="https://i.ibb.co/KzXXdq0t/Gmail-Farmer-digital-money-transfer-logo.png" alt="Logo">
<div>
<div id="siteName" style="font-size:16px;font-weight:700;color:#0037dd">Fast & Secure Exchange</div>
<div id="siteTagline" class="small">সকাল৯ঃ০০টা থেকে রাত১০ঃ০০টা</div>
</div>
</div>
<div class="top-buttons">
<span id="opStatus" class="status-badge offline">Offline</span>
<button id="myAccountBtn" onclick="openAccountModal()">My Account</button>
</div>
</div>

<div class="blue-head">
<h1 id="welcomeTitle">Welcome to Dollar Exchange</h1>
<p id="welcomeSubtitle" class="small" style="color:#e5efff">দয়া করে ট্রানজেকশন শুরু করার আগে নিয়মগুলো পড়ে নিন</p>
</div>

<div id="animatedTextBar" class="animated-text-bar" style="display:none"><span id="animatedTextSpan"></span></div>

<div id="nav">
<button id="navButton" onclick="showUser()">নগদ বিকাশ 5 টাকা সেন্ড মানি ফি কেটে নেওয়া হয়</button>
<button class="menu-btn" onclick="goMyOrders()">📦 অর্ডার</button>
<button class="menu-btn" onclick="goLiveOrders()">🔴 লাইভ অর্ডার</button>
</div>

<!-- USER AREA -->
<div id="userArea">

<div class="card">
<div id="orderInstructions" style="margin-bottom:15px; padding:12px 14px; background:#f0f9ff; border:1px solid #bae6fd; border-radius:12px; display:none;">
<h4 style="margin:0 0 6px">📌 Order Instructions</h4>
<p id="orderInstructionsText" style="margin:0"></p>
</div>

<div class="card-title">💱 অর্ডার করুন</div>

<div class="trade-type-toggle">
<button id="bhaiButton" class="active" onclick="setTradeType('bhai')">buy</button>
<button id="saleButton" onclick="setTradeType('sale')">sell</button>
</div>

<label>আপনার নাম</label>
<input id="uName" placeholder="আপনার নাম লিখুন" />

<label>কারেন্সি সিলেক্ট করুন</label>
<select id="uCurrency" onchange="updatePlaceholderText()">
</select>

<!-- ডলার পাঠানোর আইডি বক্স -->
<div id="payInfoBox" class="pay-info" style="display:none"></div>

<label>ডলার পরিমাণ</label>
<input id="uDollar" type="number" placeholder="কত ডলার সেল দিবেন (minimum 1 dollar)" oninput="calc()" />
<label>টাকায় মূল্য</label>
<input id="uTaka" placeholder="টাকায় মূল্য" readonly />

<div id="feeInfo" class="fee-box" style="display:none;">
<div>Transaction Fee: <b><span id="transactionFeeAmount">0</span> Tk</b> (<span id="transactionFeePercent">0</span>%)</div>
<div>Total Amount: <b><span id="totalAmount">0</span> Tk</b></div>
</div>

<label>মাধ্যম সিলেক্ট করুন (বিকাশ / নগদ / রকেট)</label>
<select id="uPayment">
</select>

<label>আপনার পেমেন্ট নম্বর</label>
<input id="uNumber" placeholder="আপনার পেমেন্ট নাম্বার লিখুন" />

<label>ট্রানজেকশন আইডি (ঐচ্ছিক)</label>
<input id="uTx" placeholder="এই অপশনে কিছু লিখতে হবে না">

<button class="primary" onclick="placeOrder()">🚀 অর্ডার দিন</button>
</div>

<div id="myOrdersSection">
<div class="card" style="padding:8px 18px 14px">
<div class="card-title" style="justify-content:center">📦 আপনার অর্ডারসমূহ</div>
<div id="myOrders"></div>
</div>
</div>
</div>

<!-- ===== 🔴 LIVE ORDERS (ট্রাস্ট ডিজাইন — রিয়েল-টাইম) ===== -->
<div class="card" id="liveOrdersCard">
  <div style="text-align:center"><span class="live-badge"><span class="live-dot"></span> LIVE ORDERS</span></div>
  <div class="live-sub">⚡ রিয়েল-টাইমে আপডেট হয় • সর্বশেষ ১০টি অর্ডার</div>
  <div class="trust-stats" id="trustStats">
    <div class="tstat"><h4 id="tsCompleted">—</h4><div>✅ সম্পন্ন অর্ডার</div></div>
    <div class="tstat"><h4 id="tsRate">—</h4><div>📈 সাকসেস রেট</div></div>
    <div class="tstat"><h4 id="tsUsd">—</h4><div>💰 মোট USD ট্রেড</div></div>
  </div>
  <div id="liveOrdersList"><div class="order-empty">লোড হচ্ছে...</div></div>
</div>

<div class="card" id="quoteBox" style="display:none">
  <div id="quoteText" class="quote-text"></div>
</div>

<div class="card" id="homeContentCard" style="display:none;white-space:pre-wrap"></div>

<div class="card" id="rulesSection" style="display:none">
  <h3 id="rulesTitleText" class="card-title" style="justify-content:center">📋 Exchange Rules</h3>
  <div id="rulesContentText" style="white-space:pre-wrap"></div>
</div>

<!-- ORDER DETAILS MODAL -->
<div id="modal" style="display:none;">
<div class="modal" onclick="closeModal(event)">
<div class="box" onclick="event.stopPropagation()">
<h3 id="mTitle">Order Details</h3>
<div id="mBody"></div>
<div style="margin-top:12px">
<label>ট্রানজেকশন আইডি</label>
<input id="mTx" placeholder="ট্রানজেকশন আইডি দিন">
<button class="primary" style="margin-top:10px" onclick="saveTx()">💾 সংরক্ষণ</button>
</div>
<div style="margin-top:12px;text-align:right"><button class="btn-ghost" onclick="closeModal()">Close</button></div>
</div>
</div>
</div>

<!-- CONFIRM ORDER MODAL -->
<div id="confirmModal" style="display:none;">
<div class="modal" onclick="closeConfirm(event)">
<div class="box" onclick="event.stopPropagation()">
<h3>✅ Confirm Your Order</h3>
<div id="cBody"></div>
<label>আপনার Transaction ID</label>
<input id="cTx" placeholder="আপনার Transaction ID লিখুন" />
<button class="primary" onclick="confirmOrder()">Confirm Order</button>
<div style="margin-top:12px;text-align:right"><button class="btn-ghost" onclick="closeConfirm()">Close</button></div>
</div>
</div>
</div>

<!-- WhatsApp Button (ছবি Admin Panel থেকে বদলানো যাবে) -->
<a id="whatsappLink" href="https://wa.me/qr/DTBEJ472LPKOA1" class="wa-btn" target="_blank">
<img id="whatsappImg" src="https://i.ibb.co/dnLD0Wf/20251129-064417.jpg" alt="wa">
</a>

<footer>
<b id="footerName">Fast & Secure Exchange</b> — Fast & Secure Dollar Exchange Service<br>
<span class="small">© <span id="footerYear"></span> All rights reserved</span>
</footer>

<script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore-compat.js"></script>
<script>
const TELEGRAM_BOT_TOKEN = "8585021424:AAGsqk3Tsay2y3PZVolWE-rvUjre9h0u8HQ";
const TELEGRAM_CHAT_ID = "7427334644";

const firebaseConfig = {
  apiKey: "AIzaSyAIEGcuV2Os_rqKrpa1ioWy0l0iJI060QM",
  authDomain: "saimon-f4236.firebaseapp.com",
  projectId: "saimon-f4236",
  storageBucket: "saimon-f4236.firebasestorage.app",
  messagingSenderId: "93804376133",
  appId: "1:93804376133:web:38a83389901b4699b0732c"
};

firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

const modal = document.getElementById('modal');
const confirmModal = document.getElementById('confirmModal');
const accountModal = document.getElementById('accountModal');

let currencies = [
{ id: 'Payeer', name: 'Payeer', buyRate: 68, sellRate: 70, paymentId: 'P1131698605', image: 'https://i.ibb.co/6yJ1s7Q/payeer-logo.png', minDollar: 5, maxDollar: 500 },
{ id: 'Binance', name: 'Binance', buyRate: 19, sellRate: 20, paymentId: '1188473082', image: 'https://i.ibb.co/k3QJz5w/binance-logo.png', minDollar: 1, maxDollar: 1000 },
{ id: 'Advcash', name: 'Advcash', buyRate: 58, sellRate: 60, paymentId: 'U 1048 5654 4714', image: 'https://i.ibb.co/1n1J7r6/advcash-logo.png', minDollar: 10, maxDollar: 300 }
];

let paymentMethods = [];
let quotes = [];
let quoteTimer = null;

let siteSettings = {
name: 'Fast & Secure Exchange', tagline: 'সকাল৯ঃ০০টা থেকে রাত১০ঃ০০টা', primaryColor: '#0b75ff', secondaryColor: '#0037dd',
backgroundColor: '#f2f5f8', workStartHour: 9, workEndHour: 22, workStartTime: '', workEndTime: '',
statusOverrideEnabled: false, statusOverride: '', orderInstructions: '',
whatsappLink: 'https://wa.me/qr/DTBEJ472LPKOA1', whatsappImageUrl: '', contactEmail: '', contactPhone: '', minDollarAmount: 1, maxDollarAmount: 1000,
transactionFee: 0, transactionFeePercent: 0, logoUrl: 'https://i.ibb.co.com/DD3h4qjv/file-000000007d947207b10fa3593fc67aa8.png',
faviconUrl: '', maintenanceMode: false, maintenanceMessage: 'We are currently performing maintenance. Please check back later.', requireLogin: false, showLoading: true
};

let contentSettings = {
welcomeTitle: 'Welcome to Dollar Exchange', welcomeSubtitle: 'দয়া করে ট্রানজেকশন শুরু করার আগে নিয়মগুলো পড়ে নিন',
navButtonText: 'নগদ বিকাশ 5 টাকা সেন্ড মানি ফি কেটে নেওয়া হয়', homeContent: '', rulesTitle: 'Exchange Rules',
rulesContent: 'Please read all rules before making a transaction.', globalNotification: '', notificationType: 'info',
notificationActive: false, typingText: '', typingSpeed: 80
};

let animationSettings = { loadingText: 'লোড হচ্ছে...', spinnerColor: '#0b75ff', showLoadingAll: true, animatedTextEnabled: false, animatedText: '', animationSpeed: 20, animationDirection: 'right', animatedTextColor: '#ffffff', animatedBgColor: '#0037dd' };

let currentTradeType = 'bhai';

function escapeHtml(v){ return String(v == null ? '' : v).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }

// ==========================================
// ✅ COPY SYSTEM (সম্পূর্ণ ফিক্স — HTTPS ছাড়াও কাজ করবে)
// ==========================================
function fallbackCopy(str, onSuccess){
  try{
    const ta = document.createElement('textarea');
    ta.value = str;
    ta.style.position = 'fixed'; ta.style.top = '-9999px'; ta.style.opacity = '0';
    document.body.appendChild(ta);
    ta.focus(); ta.select();
    document.execCommand('copy');
    document.body.removeChild(ta);
    onSuccess();
  }catch(err){
    prompt('ম্যানুয়ালি কপি করুন (Ctrl+C চাপুন):', str);
  }
}
function doCopy(str, onSuccess){
  str = String(str || '');
  if(navigator.clipboard && window.isSecureContext){
    navigator.clipboard.writeText(str).then(onSuccess).catch(() => fallbackCopy(str, onSuccess));
  } else { fallbackCopy(str, onSuccess); }
}
// সব [data-copy] বাটনে এক ক্লিক লিসেনার — কোথাও বসালেই কাজ করবে
document.addEventListener('click', function(e){
  const btn = e.target.closest('[data-copy]');
  if(!btn) return;
  doCopy(btn.getAttribute('data-copy'), () => {
    const old = btn.innerHTML;
    btn.innerHTML = '✔ Copied!';
    btn.classList.add('copied');
    setTimeout(() => { btn.innerHTML = old; btn.classList.remove('copied'); }, 1500);
  });
});

// ==========================================
// মেনু নেভিগেশন
// ==========================================
function scrollToSection(id){
  const el = document.getElementById(id);
  if(el) el.scrollIntoView({ behavior: 'smooth', block: 'start' });
}
function goMyOrders(){ loadMyOrders(); scrollToSection('myOrdersSection'); }
function goLiveOrders(){ scrollToSection('liveOrdersCard'); }

// ডলার পাঠানোর আইডি বক্স
function updatePayInfo(){
  const box = document.getElementById('payInfoBox');
  const currency = currencies.find(c => c.id === uCurrency.value);
  if(currency && currency.paymentId){
    box.innerHTML = `<div class="pay-label">💵 ডলার পাঠানোর আইডি (${escapeHtml(currency.name)}):</div>
    <div class="pay-id-row"><b>${escapeHtml(currency.paymentId)}</b><button class="copy-btn-inside" data-copy="${escapeHtml(currency.paymentId)}">📋 Copy</button></div>`;
    box.style.display = 'block';
  } else { box.style.display = 'none'; }
}

// ==========================================
// ব্রাউজার নোটিফিকেশন (ইউজারের জন্য)
// ==========================================
function initBrowserNotifications() {
    if (!("Notification" in window)) { return; }
    else if (Notification.permission !== "granted" && Notification.permission !== "denied") {
        Notification.requestPermission().then(function (permission) {
            if (permission === "granted") { console.log("Notification permission granted."); }
        });
    }
}
function showUserNotification(title, body) {
    if (Notification.permission === "granted") {
        new Notification(title, {
            body: body,
            icon: siteSettings.logoUrl || 'https://i.ibb.co.com/DD3h4qjv/file-000000007d947207b10fa3593fc67aa8.png',
            vibrate: [200, 100, 200],
            tag: "order-status-update"
        });
    }
}

function listenForOrderUpdates() {
    const current = getCurrentUser();
    if (!current) return;
    db.collection('orders').where('userEmail', '==', current.email)
    .onSnapshot(snapshot => {
        snapshot.docChanges().forEach(change => {
            if (change.type === "modified") {
                const order = change.doc.data();
                let msg = "";
                if(order.status === "COMPLETED") {
                    msg = `অভিনন্দন! আপনার ${order.dollar}$ এর অর্ডারটি সফলভাবে সম্পন্ন হয়েছে।`;
                    showUserNotification("✅ Order Completed", msg);
                } else if(order.status === "REJECTED") {
                    msg = `দুঃখিত, আপনার অর্ডারটি বাতিল করা হয়েছে।`;
                    showUserNotification("❌ Order Rejected", msg);
                }
            }
        });
    });
}

// ==========================================
// 🔴 LIVE ORDERS + ট্রাস্ট স্ট্যাটস (রিয়েল-টাইম)
// ==========================================
let liveOrdersPrevIds = new Set();

function timeAgo(iso){
  const diff = Date.now() - new Date(iso).getTime();
  if(!isFinite(diff) || diff < 0) return '';
  const m = Math.floor(diff/60000);
  if(m < 1) return 'এইমাত্র';
  if(m < 60) return m + ' মিনিট আগে';
  const h = Math.floor(m/60);
  if(h < 24) return h + ' ঘণ্টা আগে';
  return Math.floor(h/24) + ' দিন আগে';
}

function maskName(name){
    const n = String(name || '').trim();
    if(!n) return 'Anonymous';
    if(n.length <= 2) return n.charAt(0) + '***';
    return n.charAt(0) + '***' + n.charAt(n.length - 1);
}
function maskNumber(num){
    const s = String(num || '').trim();
    if(!s) return '';
    if(s.length < 8) return '***';
    return s.slice(0, 3) + '****' + s.slice(-4);
}

function initLiveOrders(){
    db.collection('orders').orderBy('createdAt', 'desc').limit(10).onSnapshot(snapshot => {
        renderLiveOrders(snapshot.docs.map(d => ({ id: d.id, ...d.data() })));
        loadTrustStats(); // স্ট্যাটস আপডেট রাখে
    }, err => {
        console.error("Live orders error:", err);
        db.collection('orders').onSnapshot(snapshot => {
            const orders = snapshot.docs.map(d => ({ id: d.id, ...d.data() }));
            orders.sort((a, b) => new Date(b.createdAt || 0) - new Date(a.createdAt || 0));
            renderLiveOrders(orders.slice(0, 10));
            loadTrustStats();
        }, err2 => {
            console.error("Live orders fallback error:", err2);
            const c = document.getElementById('liveOrdersList');
            if(c) c.innerHTML = '<div class="order-empty">লাইভ অর্ডার লোড করা যাচ্ছে না</div>';
        });
    });
}

// ট্রাস্ট স্ট্যাটস: মোট সম্পন্ন, সাকসেস রেট, মোট USD
async function loadTrustStats(){
  try{
    const snap = await db.collection('orders').get();
    let completed = 0, total = 0, usd = 0;
    snap.forEach(d => {
      const o = d.data(); total++;
      if(String(o.status || '').toUpperCase() === 'COMPLETED'){ completed++; usd += Number(o.dollar) || 0; }
    });
    const rate = total ? Math.round(completed / total * 100) : 100;
    const e1 = document.getElementById('tsCompleted'), e2 = document.getElementById('tsRate'), e3 = document.getElementById('tsUsd');
    if(e1) e1.textContent = completed;
    if(e2) e2.textContent = rate + '%';
    if(e3) e3.textContent = usd >= 1000 ? (usd/1000).toFixed(1) + 'K' : usd;
  }catch(e){ console.error("Trust stats error:", e); }
}

function renderLiveOrders(orders){
    const container = document.getElementById('liveOrdersList');
    if(!container) return;
    if(!orders.length){
        container.innerHTML = '<div class="order-empty">এখনো কোনো অর্ডার হয়নি — প্রথম অর্ডারটি আপনিই দিতে পারেন! 😊</div>';
        liveOrdersPrevIds = new Set();
        return;
    }
    container.innerHTML = orders.map(o => {
        const s = getBanglaStatus(o.status);
        const isDone = s.cls === 'completed';
        const masked = maskName(o.name);
        const ago = o.createdAt ? timeAgo(o.createdAt) : '';
        const isNew = liveOrdersPrevIds.size > 0 && !liveOrdersPrevIds.has(o.id);
        return `<div class="live-order-item${isNew ? ' live-new' : ''}">
            <div class="lo-avatar${isDone ? ' lo-done' : ''}">${escapeHtml(masked.charAt(0).toUpperCase())}${isDone ? '<span class="lo-verified">✔</span>' : ''}</div>
            <div class="lo-main">
                <b>${escapeHtml(masked)}</b> ${isDone ? '<span style="color:#16a34a;font-weight:700;font-size:12px">✔ Verified Trade</span>' : ''}
                <div class="small">📱 ${escapeHtml(maskNumber(o.number))}</div>
                <div class="small">${escapeHtml(o.currency || '')} • ${escapeHtml(String(o.dollar ?? ''))} USD → ${escapeHtml(String(o.taka ?? ''))} TK</div>
            </div>
            <div class="lo-right">
                <span class="status ${s.cls}">${s.text}</span>
                <div class="lo-time">🕘 ${escapeHtml(ago)}</div>
            </div>
        </div>`;
    }).join('');
    liveOrdersPrevIds = new Set(orders.map(o => o.id));
}

// TELEGRAM (ADMIN) — অর্ডার হলেই টেলিগ্রামে যাবে (২৪/৭)
async function sendTelegramNotification(orderDetails) {
    const message = `
🔔 *New Order Received!*

👤 *Name:* ${orderDetails.name}
📱 *Phone:* ${orderDetails.number}
💱 *Type:* ${orderDetails.tradeType}
💸 *Amount:* ${orderDetails.dollar}$ = ${orderDetails.taka} Tk
📦 *Currency:* ${orderDetails.currency}
💳 *Medium:* ${orderDetails.paymentMethod || ''}
🆔 *TXID:* ${orderDetails.trx}

⏰ *Time:* ${new Date().toLocaleString()}
    `;
    const url = `https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage`;
    try {
        await fetch(url, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ chat_id: TELEGRAM_CHAT_ID, text: message, parse_mode: "Markdown" })
        });
    } catch (e) { console.error("Telegram Error:", e); }
}

// ACCOUNT FUNCTIONS
function openAccountModal(){ accountModal.style.display = "flex"; document.body.classList.add('modal-open'); updateAccountUI(); }
function closeAccountModal(){ accountModal.style.display = "none"; document.body.classList.remove('modal-open'); }
function showSignup(){ loginForm.style.display='none'; signupForm.style.display='block'; fisherForm.style.display='none'; forgotPasswordForm.style.display='none'; accProfile.style.display='none'; accTitle.innerText = 'Sign Up'; }
function showLogin(){ loginForm.style.display='block'; signupForm.style.display='none'; fisherForm.style.display='none'; forgotPasswordForm.style.display='none'; accProfile.style.display='none'; accTitle.innerText = 'Login'; }
function showFisher(){ loginForm.style.display='none'; signupForm.style.display='none'; fisherForm.style.display='block'; forgotPasswordForm.style.display='none'; accProfile.style.display='none'; accTitle.innerText = 'Fisher Sign Up'; }
function showForgotPassword(){ loginForm.style.display='none'; signupForm.style.display='none'; fisherForm.style.display='none'; forgotPasswordForm.style.display='block'; accProfile.style.display='none'; accTitle.innerText = 'Reset Password'; }

async function signupUser(){
const name = signupName.value.trim();
const email = signupEmail.value.trim().toLowerCase();
const number = signupNumber.value.trim();
const pass = signupPassword.value;
if(!name || !email || !pass || !number){ alert('সব ঘর পূরণ করুন'); return; }
try {
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (!userSnapshot.empty) { alert('এই ইমেইল দিয়ে আগে থেকেই অ্যাকাউন্ট আছে'); return; }
await db.collection('users').add({ name, email, number, password: pass, userType: 'regular', createdAt: new Date().toISOString() });
localStorage.setItem('currentUser', JSON.stringify({ name, email, number, userType: 'regular' }));
signupName.value=''; signupEmail.value=''; signupNumber.value=''; signupPassword.value='';
updateAccountUI(); closeAccountModal(); alert('Account created and logged in ✔'); prefillUserFields(); loadMyOrders();
listenForOrderUpdates();
} catch (error) { console.error("Error creating user:", error); alert("Error creating account. Please try again."); }
}

async function signupFisher(){
const name = fisherName.value.trim();
const email = fisherEmail.value.trim().toLowerCase();
const number = fisherNumber.value.trim();
const pass = fisherPassword.value;
if(!name || !email || !pass || !number){ alert('সব ঘর পূরণ করুন'); return; }
try {
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (!userSnapshot.empty) { alert('এই ইমেইল দিয়ে আগে থেকেই অ্যাকাউন্ট আছে'); return; }
await db.collection('users').add({ name, email, number, password: pass, userType: 'fisher', createdAt: new Date().toISOString() });
localStorage.setItem('currentUser', JSON.stringify({ name, email, number, userType: 'fisher' }));
fisherName.value=''; fisherEmail.value=''; fisherNumber.value=''; fisherPassword.value='';
updateAccountUI(); closeAccountModal(); alert('Fisher Account created and logged in ✔'); prefillUserFields(); loadMyOrders();
listenForOrderUpdates();
} catch (error) { console.error("Error creating fisher account:", error); alert("Error creating fisher account. Please try again."); }
}

async function loginUser(){
const email = loginEmail.value.trim().toLowerCase();
const pass = loginPassword.value;
try {
const userSnapshot = await db.collection('users').where('email', '==', email).where('password', '==', pass).get();
if (userSnapshot.empty) { alert('Invalid credentials'); return; }
const user = userSnapshot.docs[0].data();
localStorage.setItem('currentUser', JSON.stringify({ name: user.name, email: user.email, number: user.number, userType: user.userType || 'regular' }));
updateAccountUI(); closeAccountModal(); alert('Login successful ✔'); prefillUserFields(); loadMyOrders();
listenForOrderUpdates();
} catch (error) { console.error("Error logging in:", error); alert("Error logging in. Please try again."); }
}

function logoutUser(){ localStorage.removeItem('currentUser'); updateAccountUI(); alert('Logged out'); uName.value=''; uNumber.value=''; loadMyOrders(); }
function getCurrentUser(){ return JSON.parse(localStorage.getItem('currentUser')||'null'); }

function updateAccountUI(){
const u = getCurrentUser();
if(u){
accProfile.style.display='block'; loginForm.style.display='none'; signupForm.style.display='none'; fisherForm.style.display='none'; forgotPasswordForm.style.display='none'; accTitle.innerText = 'Account';
pName.innerText = u.name; pEmail.innerText = u.email; pNumber.innerText = u.number; myAccountBtn.innerText = 'Account ✓';
} else {
accProfile.style.display='none'; loginForm.style.display='block'; signupForm.style.display='none'; fisherForm.style.display='none'; forgotPasswordForm.style.display='none'; accTitle.innerText = 'Login'; myAccountBtn.innerText = 'My Account';
}
}

function prefillUserFields(){
const u = getCurrentUser();
if(u){ uName.value = u.name || ''; uNumber.value = u.number || ''; }
}

async function sendPasswordReset() {
const email = forgotEmail.value.trim().toLowerCase();
if (!email) { alert('Please enter your email address'); return; }
try {
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (userSnapshot.empty) { alert('No account found with this email address'); return; }
const resetCode = Math.floor(100000 + Math.random() * 900000).toString();
const expiryTime = new Date(Date.now() + 3600000).toISOString();
await db.collection('passwordResets').add({ email, resetCode, expiryTime, used: false });
document.getElementById('resetCodeSection').style.display = 'block';
alert(`A verification code has been sent to your email. For demo purposes, your code is: ${resetCode}`);
} catch (error) { console.error("Error sending password reset:", error); alert("Error sending password reset. Please try again."); }
}

async function resetPassword() {
const email = forgotEmail.value.trim().toLowerCase();
const code = resetCode.value.trim();
const newPassword = resetNewPassword.value;
if (!email || !code || !newPassword) { alert('Please fill all fields'); return; }
try {
const resetSnapshot = await db.collection('passwordResets').where('email', '==', email).where('resetCode', '==', code).where('used', '==', false).get();
if (resetSnapshot.empty) { alert('Invalid or expired verification code'); return; }
const resetDoc = resetSnapshot.docs[0];
const resetData = resetDoc.data();
if (new Date() > new Date(resetData.expiryTime)) { alert('Verification code has expired'); return; }
await db.collection('passwordResets').doc(resetDoc.id).update({ used: true });
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (!userSnapshot.empty) { const userDoc = userSnapshot.docs[0]; await db.collection('users').doc(userDoc.id).update({ password: newPassword }); }
forgotEmail.value = ''; resetCode.value = ''; resetNewPassword.value = '';
document.getElementById('resetCodeSection').style.display = 'none';
alert('Password reset successful! You can now login with your new password.');
showLogin();
} catch (error) { console.error("Error resetting password:", error); alert("Error resetting password. Please try again."); }
}

// LOAD SETTINGS
async function loadSiteSettings() {
try {
const settingsDoc = await db.collection('settings').doc('site').get();
if (settingsDoc.exists) { siteSettings = { ...siteSettings, ...settingsDoc.data() }; }
} catch (error) { console.error("Error loading site settings:", error); }
applySiteSettings();
}

async function loadContentSettings() {
try {
const contentDoc = await db.collection('settings').doc('content').get();
if (contentDoc.exists) { contentSettings = { ...contentSettings, ...contentDoc.data() }; }
} catch (error) { console.error("Error loading content settings:", error); }
applyContentSettings();
}

async function loadAnimationSettings() {
try {
const aDoc = await db.collection('settings').doc('animations').get();
if (aDoc.exists) { animationSettings = { ...animationSettings, ...aDoc.data() }; }
} catch (error) { console.error("Error loading animation settings:", error); }
applyAnimationSettings();
}

async function loadQuotes() {
try {
const qDoc = await db.collection('settings').doc('quotes').get();
if (qDoc.exists && Array.isArray(qDoc.data().list)) { quotes = qDoc.data().list; }
} catch (error) { console.error("Error loading quotes:", error); }
startQuoteRotation();
}

async function loadPaymentMethods() {
try {
const paymentMethodsDoc = await db.collection('settings').doc('paymentMethods').get();
if (paymentMethodsDoc.exists && Array.isArray(paymentMethodsDoc.data().list) && paymentMethodsDoc.data().list.length) {
paymentMethods = paymentMethodsDoc.data().list;
}
} catch (error) { console.error("Error loading payment methods:", error); }
updatePaymentMethods();
}

function getWorkHours(){
  if(siteSettings.workStartHour != null && siteSettings.workStartHour !== '' && siteSettings.workEndHour != null && siteSettings.workEndHour !== ''){
    return { startMinutes: Number(siteSettings.workStartHour) * 60, endMinutes: Number(siteSettings.workEndHour) * 60, startLabel: siteSettings.workStartHour + ':00', endLabel: siteSettings.workEndHour + ':00' };
  }
  if(siteSettings.workStartTime && siteSettings.workEndTime){
    const [sh, sm] = String(siteSettings.workStartTime).split(':').map(Number);
    const [eh, em] = String(siteSettings.workEndTime).split(':').map(Number);
    return { startMinutes: (sh || 0) * 60 + (sm || 0), endMinutes: (eh || 0) * 60 + (em || 0), startLabel: siteSettings.workStartTime, endLabel: siteSettings.workEndTime };
  }
  return { startMinutes: 9 * 60, endMinutes: 22 * 60, startLabel: '09:00', endLabel: '22:00' };
}

function applySiteSettings() {
document.title = siteSettings.name || 'Dollar Exchange';
document.getElementById('pageTitle').textContent = siteSettings.name || 'Dollar Exchange';
if (siteSettings.faviconUrl) { document.getElementById('favicon').href = siteSettings.faviconUrl; }
if (siteSettings.logoUrl) { document.getElementById('logoImg').src = siteSettings.logoUrl; }
document.getElementById('siteName').textContent = siteSettings.name;
document.getElementById('footerName').textContent = siteSettings.name;
// ✅ WhatsApp লিংক + বাটনের ছবি (Admin Panel থেকে বদলানো যায়)
if (siteSettings.whatsappLink) { document.getElementById('whatsappLink').href = siteSettings.whatsappLink; }
if (siteSettings.whatsappImageUrl) { document.getElementById('whatsappImg').src = siteSettings.whatsappImageUrl; }
const wh = getWorkHours();
document.getElementById('siteTagline').textContent = (siteSettings.tagline ? siteSettings.tagline + ' • ' : '') + `🕘 ${wh.startLabel} - ${wh.endLabel}`;
document.documentElement.style.setProperty('--primary', siteSettings.primaryColor);
document.documentElement.style.setProperty('--secondary', siteSettings.secondaryColor);
document.body.style.backgroundColor = siteSettings.backgroundColor;
document.querySelectorAll('.primary').forEach(el => { el.style.background = `linear-gradient(135deg,${siteSettings.primaryColor},${siteSettings.secondaryColor})`; });
document.querySelectorAll('.top-buttons button').forEach(el => { el.style.borderColor = siteSettings.primaryColor; el.style.color = siteSettings.primaryColor; });
document.querySelector('.blue-head').style.background = `linear-gradient(135deg,${siteSettings.secondaryColor},${siteSettings.primaryColor})`;
if (siteSettings.orderInstructions) { document.getElementById('orderInstructions').style.display = 'block'; document.getElementById('orderInstructionsText').textContent = siteSettings.orderInstructions; }
if (siteSettings.maintenanceMode) { document.getElementById('maintenanceOverlay').style.display = 'flex'; document.getElementById('maintenanceMessage').textContent = siteSettings.maintenanceMessage; }
}

function applyContentSettings() {
document.getElementById('welcomeTitle').textContent = contentSettings.welcomeTitle;
document.getElementById('welcomeSubtitle').textContent = contentSettings.welcomeSubtitle;
document.getElementById('navButton').textContent = contentSettings.navButtonText;

if (contentSettings.globalNotification && contentSettings.notificationActive) {
const notificationEl = document.getElementById('globalNotification');
notificationEl.textContent = contentSettings.globalNotification;
notificationEl.className = `global-notification notification-${contentSettings.notificationType}`;
notificationEl.style.display = 'block';
}

const homeCard = document.getElementById('homeContentCard');
if (contentSettings.homeContent) { homeCard.style.display = 'block'; homeCard.textContent = contentSettings.homeContent; }
else { homeCard.style.display = 'none'; }

const rulesSection = document.getElementById('rulesSection');
if (contentSettings.rulesContent) {
rulesSection.style.display = 'block';
document.getElementById('rulesTitleText').textContent = '📋 ' + (contentSettings.rulesTitle || 'Exchange Rules');
document.getElementById('rulesContentText').textContent = contentSettings.rulesContent;
} else { rulesSection.style.display = 'none'; }

if (contentSettings.typingText) {
   startTypingAnimation(contentSettings.typingText, contentSettings.typingSpeed || 80);
}
}

function applyAnimationSettings() {
const loadingTextEl = document.querySelector('.loading-text');
const loaderEl = document.querySelector('.loader');
if (loadingTextEl) loadingTextEl.textContent = animationSettings.loadingText || 'লোড হচ্ছে...';
if (loaderEl) loaderEl.style.borderTopColor = animationSettings.spinnerColor || '#0b75ff';

const bar = document.getElementById('animatedTextBar');
const span = document.getElementById('animatedTextSpan');
if (animationSettings.animatedTextEnabled && animationSettings.animatedText && String(animationSettings.animatedText).trim()) {
bar.style.display = 'block';
bar.style.background = animationSettings.animatedBgColor || '#0037dd';
span.textContent = animationSettings.animatedText;
span.style.color = animationSettings.animatedTextColor || '#ffffff';
const speed = Math.min(60, Math.max(5, Number(animationSettings.animationSpeed) || 20));
span.style.animation = `scrollText ${speed}s linear infinite`;
span.style.animationDirection = animationSettings.animationDirection === 'left' ? 'reverse' : 'normal';
} else { bar.style.display = 'none'; }
}

function startQuoteRotation() {
const box = document.getElementById('quoteBox');
const textEl = document.getElementById('quoteText');
if (!box || !textEl) return;
if (quoteTimer) { clearInterval(quoteTimer); quoteTimer = null; }
if (!quotes.length) { box.style.display = 'none'; return; }
box.style.display = 'block';
let i = 0;
const show = () => {
const q = quotes[i % quotes.length];
textEl.innerHTML = `“${escapeHtml(q.text)}”` + (q.author ? `<div class="quote-author">— ${escapeHtml(q.author)}</div>` : '');
i++;
};
show();
quoteTimer = setInterval(show, 8000);
}

function updatePaymentMethods() {
const uPayment = document.getElementById('uPayment');
const defaults = [{ id: 'bKash', name: 'bKash' }, { id: 'Nagad', name: 'Nagad' }, { id: 'Rocket', name: 'Rocket' }];
let list = [...paymentMethods];
defaults.forEach(d => { if (!list.some(m => String(m.name || m.id).toLowerCase() === d.name.toLowerCase())) list.push(d); });
uPayment.innerHTML = '';
list.forEach(method => {
const option = document.createElement('option');
option.value = method.name || method.id;
option.textContent = method.name || method.id;
uPayment.appendChild(option);
});
}

async function loadCurrencies(){
try {
const currenciesDoc = await db.collection('settings').doc('currencies').get();
if (currenciesDoc.exists) {
const loadedCurrencies = currenciesDoc.data().list || currencies;
currencies = loadedCurrencies.map(currency => ({ ...currency, minDollar: currency.minDollar || siteSettings.minDollarAmount || 1, maxDollar: currency.maxDollar || siteSettings.maxDollarAmount || 1000 }));
}
} catch (error) { console.error("Error loading currencies:", error); }
const uCurrency = document.getElementById('uCurrency');
uCurrency.innerHTML = '';
currencies.forEach(currency => {
const option = document.createElement('option');
option.value = currency.id;
const rate = currentTradeType === 'bhai' ? (currency.buyRate || currency.rate) : (currency.sellRate || currency.rate);
option.textContent = `${currency.name} (${rate} BDT)`;
uCurrency.appendChild(option);
});
if (uDollar.value) { calc(); }
updatePayInfo();
}

function setTradeType(type) {
currentTradeType = type;
document.getElementById('bhaiButton').classList.toggle('active', type === 'bhai');
document.getElementById('saleButton').classList.toggle('active', type === 'sale');
loadCurrencies();
}

function calc(){
const dollar = Number(uDollar.value) || 0;
const currencyId = uCurrency.value;
const currency = currencies.find(c => c.id === currencyId);
const rate = currency ? (currentTradeType === 'bhai' ? (currency.buyRate || currency.rate) : (currency.sellRate || currency.rate)) : 0;
const taka = dollar * rate;
uTaka.value = taka.toFixed(2);
if (siteSettings.transactionFee > 0 || siteSettings.transactionFeePercent > 0) {
const feeFixed = siteSettings.transactionFee || 0;
const feePercent = siteSettings.transactionFeePercent || 0;
const feeAmount = feeFixed + (taka * feePercent / 100);
const total = taka + feeAmount;
document.getElementById('feeInfo').style.display = 'block';
document.getElementById('transactionFeeAmount').textContent = feeAmount.toFixed(2);
document.getElementById('transactionFeePercent').textContent = feePercent;
document.getElementById('totalAmount').textContent = total.toFixed(2);
} else { document.getElementById('feeInfo').style.display = 'none'; }
}

function updatePlaceholderText() {
const currencyId = uCurrency.value;
const currency = currencies.find(c => c.id === currencyId);
calc();
updatePayInfo();
if (currency) {
const minLimit = currency.minDollar || siteSettings.minDollarAmount;
const maxLimit = currency.maxDollar || siteSettings.maxDollarAmount;
uDollar.placeholder = `কত ডলার সেল দিবেন (${minLimit} থেকে ${maxLimit} ডলার পর্যন্ত)`;
} else { uDollar.placeholder = `কত ডলার সেল দিবেন (minimum ${siteSettings.minDollarAmount} dollar)`; }
}

function placeOrder(){
const current = getCurrentUser();
if(siteSettings.requireLogin && !current){ alert('অর্ডার দিতে হলে প্রথমে Login/Sign Up করুন'); openAccountModal(); return; }
const name = (uName.value.trim() || current?.name);
const number = (uNumber.value.trim() || current?.number);
const currencyId = uCurrency.value;
const currency = currencies.find(c => c.id === currencyId);
const currencyName = currency ? currency.name : '';
const dollar = parseFloat(uDollar.value);
const taka = uTaka.value;
const payment = uPayment.value;
const tx = uTx.value.trim() || "";

if (currency) {
const minLimit = currency.minDollar || siteSettings.minDollarAmount;
const maxLimit = currency.maxDollar || siteSettings.maxDollarAmount;
if (dollar < minLimit) { alert(`${currencyName} এর জন্য সর্বনিম্ন ${minLimit} ডলার হতে হবে`); return; }
if (dollar > maxLimit) { alert(`${currencyName} এর জন্য সর্বোচ্চ ${maxLimit} ডলার হতে হবে`); return; }
} else {
if (dollar < siteSettings.minDollarAmount) { alert(`Minimum dollar amount is ${siteSettings.minDollarAmount}`); return; }
if (dollar > siteSettings.maxDollarAmount) { alert(`Maximum dollar amount is ${siteSettings.maxDollarAmount}`); return; }
}

if(!name || !number || !dollar){ alert('সব ঘর পূরণ করুন'); return; }

window.tempOrder = { name, number, currency: currencyName, currencyId, dollar, taka, payment, via: payment, tx, tradeType: currentTradeType };

const paymentIds = currencies.map(c => `<div class="id-badge">${escapeHtml(c.name)} ID: ${escapeHtml(c.paymentId)} <button class="copy-btn-inside" style="float:right" data-copy="${escapeHtml(c.paymentId)}">📋 Copy</button></div>`).join('');

cBody.innerHTML = `
<div>নাম: <b>${escapeHtml(name)}</b></div>
<div>নম্বার: <b>${escapeHtml(number)}</b></div>
<div>কারেন্সি: <b>${escapeHtml(currencyName)}</b></div>
<div>ডলার: <b>${escapeHtml(dollar)}</b> → টাকা: <b>${escapeHtml(taka)}</b></div>
<div>মাধ্যম: <b>${escapeHtml(payment)}</b></div>
<div>Trade Type: <b>${currentTradeType === 'bhai' ? 'Bhai Rate' : 'Sale Rate'}</b></div>
<div style="margin-top:10px;font-weight:700">পেমেন্ট পাঠানোর আইডি:</div>
 ${paymentIds}
`;
cTx.value = tx;
confirmModal.style.display = "flex";
document.body.classList.add('modal-open');
}

async function confirmOrder(){
const tx = cTx.value.trim();
const o = tempOrder;
if(!o) return;
try {
const newOrder = {
name: o.name, number: o.number, currency: o.currency, currencyId: o.currencyId, dollar: o.dollar, taka: o.taka, paymentMethod: o.payment, via: o.via || "", trx: tx || "",
status: 'PENDING', createdAt: new Date().toISOString(), userEmail: getCurrentUser() ? getCurrentUser().email : null, userType: getCurrentUser() ? getCurrentUser().userType || 'regular' : 'regular', tradeType: o.tradeType || 'sell',
telegramSent: true
};
const docRef = await db.collection('orders').add(newOrder);
newOrder.id = docRef.id;
sendTelegramNotification(newOrder);
confirmModal.style.display="none"; document.body.classList.remove('modal-open'); tempOrder=null;
loadMyOrders(); alert("অর্ডার Confirm হয়েছে ✔");
uDollar.value=""; uTaka.value=""; uTx.value="";
} catch (error) { console.error("Error creating order:", error); alert("Error creating order. Please try again."); }
}

function getBanglaStatus(status){
if(status === "COMPLETED") return { text: "✔ completed", cls: "completed" };
if(status === "REJECTED") return { text: "✘ বাতিল", cls: "rejected" };
return { text: "⌛ অপেক্ষমাণ", cls: "pending" };
}

async function loadMyOrders(){
try {
const current = getCurrentUser();
myOrders.innerHTML = "";
if(current){
const emailSnapshot = await db.collection('orders').where('userEmail', '==', current.email).get();
const numberSnapshot = await db.collection('orders').where('number', '==', current.number).get();
const allOrders = emailSnapshot.docs.map(doc => ({id: doc.id, ...doc.data()}));
numberSnapshot.docs.forEach(doc => { const d = {id: doc.id, ...doc.data()}; if (!allOrders.find(o => o.id === d.id)) { allOrders.push(d); } });
allOrders.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
renderOrders(allOrders);
} else {
const number = uNumber.value.trim();
if(number) {
const numberSnapshot = await db.collection('orders').where('number', '==', number).get();
const orders = numberSnapshot.docs.map(doc => ({id: doc.id, ...doc.data()}));
orders.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
renderOrders(orders);
} else { myOrders.innerHTML='<div class="order-empty">আপনার অর্ডার নেই</div>'; }
}
} catch (error) { console.error("Error loading orders:", error); myOrders.innerHTML='<div class="order-empty">Error loading orders</div>'; }
}

function renderOrders(orders) {
if(orders.length===0){ myOrders.innerHTML='<div class="order-empty">আপনার অর্ডার নেই</div>'; return; }
orders.forEach(o=>{
let currencyName = o.currency;
if (!currencyName && o.currencyId) { const currency = currencies.find(c => c.id === o.currencyId); currencyName = currency ? currency.name : o.currencyId; }
const s = getBanglaStatus(o.status);
const box=document.createElement('div');
box.className='order-box';
box.innerHTML=`
<div class="order-info">
<div><b>${escapeHtml(o.name)}</b> <span class="small">• ${new Date(o.createdAt).toLocaleString()}</span></div>
<div class="small">${escapeHtml(currencyName)} • ${escapeHtml(String(o.dollar))} USD → ${escapeHtml(String(o.taka))} TK</div>
<div class="small">মাধ্যম: ${escapeHtml(o.paymentMethod || o.via || 'Not given')}</div>
<div class="small">TXID: ${escapeHtml(o.trx || 'Not given')}</div>
<div class="small">Trade Type: ${o.tradeType === 'bhai' ? 'Bhai Rate' : 'Sale Rate'}</div>
</div>
<div class="order-meta">
<div><span class="status ${s.cls}">${s.text}</span></div>
<button class="btn-ghost" style="margin-top:8px;width:100%" onclick="openModal('${o.id}')">View</button>
</div>
`;
myOrders.appendChild(box);
});
}

let currentModalId=null;
async function openModal(id){
currentModalId=id;
try {
const orderDoc = await db.collection('orders').doc(id).get();
if (!orderDoc.exists) return;
const o = {id: orderDoc.id, ...orderDoc.data()};
let currencyName = o.currency;
if (!currencyName && o.currencyId) { const currency = currencies.find(c => c.id === o.currencyId); currencyName = currency ? currency.name : o.currencyId; }
mTitle.innerText="Order — "+o.name;
mBody.innerHTML=`
<div class="small">Created: ${new Date(o.createdAt).toLocaleString()}</div>
<div>নাম: <b>${escapeHtml(o.name)}</b></div>
<div>নম্বার: <b>${escapeHtml(o.number)}</b></div>
<div>কারেন্সি: <b>${escapeHtml(currencyName)}</b></div>
<div>ডলার: <b>${escapeHtml(String(o.dollar))}</b> → টাকা: <b>${escapeHtml(String(o.taka))}</b></div>
<div>মাধ্যম: <b>${escapeHtml(o.paymentMethod || o.via || 'Not given')}</b></div>
<div>Trade Type: <b>${o.tradeType === 'bhai' ? 'Bhai Rate' : 'Sale Rate'}</b></div>
<div style="margin-top:8px">বর্তমান স্ট্যাটাস: <b>${escapeHtml(o.status)}</b></div>
`;
mTx.value = o.trx || "";
modal.style.display="flex";
document.body.classList.add('modal-open');
} catch (error) { console.error("Error opening order:", error); alert("Error loading order details"); }
}

function closeModal(event){
if (!event || event.target === modal || event.target.textContent === 'Close') { modal.style.display='none'; document.body.classList.remove('modal-open'); currentModalId=null; }
}

function closeConfirm(event){
if (!event || event.target === confirmModal || event.target.textContent === 'Close') { confirmModal.style.display='none'; document.body.classList.remove('modal-open'); }
}

async function saveTx(){
if(!currentModalId) return;
const tx = mTx.value.trim();
try {
await db.collection('orders').doc(currentModalId).update({ trx: tx });
loadMyOrders(); alert("Transaction ID Updated"); closeModal();
} catch (error) { console.error("Error updating transaction ID:", error); alert("Error updating transaction ID. Please try again."); }
}

function updateStatus(){
  let isOnline = false;
  const now = new Date();
  const nowTotalMinutes = now.getHours() * 60 + now.getMinutes();
  if (siteSettings.statusOverrideEnabled) { isOnline = String(siteSettings.statusOverride) === 'online'; }
  else if (siteSettings.statusOverride === 'online') { isOnline = true; }
  else if (siteSettings.statusOverride === 'offline') { isOnline = false; }
  else {
    const wh = getWorkHours();
    if (wh.endMinutes > wh.startMinutes) { isOnline = nowTotalMinutes >= wh.startMinutes && nowTotalMinutes < wh.endMinutes; }
    else { isOnline = nowTotalMinutes >= wh.startMinutes || nowTotalMinutes < wh.endMinutes; }
  }
  if(isOnline){ opStatus.innerText='Online'; opStatus.className='status-badge online'; }
  else { opStatus.innerText='Offline'; opStatus.className='status-badge offline'; }
}
setInterval(updateStatus, 60000);
function showUser(){ userArea.style.display='block'; scrollToSection('userArea'); }

let typingInterval;
function startTypingAnimation(text, speed) {
  const element = document.getElementById('welcomeSubtitle');
  if (!element || !text) return;
  if (typingInterval) clearInterval(typingInterval);
  element.innerHTML = ''; element.classList.add('typing-text');
  let charIndex = 0;
  function type() {
    if (charIndex < text.length) { element.textContent += text.charAt(charIndex); charIndex++; }
    else { clearInterval(typingInterval); setTimeout(() => { element.textContent = ''; charIndex = 0; typingInterval = setInterval(type, speed); }, 2000); }
  }
  typingInterval = setInterval(type, speed);
}

window.addEventListener('load',async()=>{
await loadSiteSettings();
await loadContentSettings();
await loadAnimationSettings();
await loadPaymentMethods();
await loadCurrencies();
await loadQuotes();
updateAccountUI();
prefillUserFields();
loadMyOrders();
initLiveOrders();
updatePlaceholderText();
updateStatus();
document.getElementById('footerYear').textContent = new Date().getFullYear();

initBrowserNotifications();

if(getCurrentUser()) { listenForOrderUpdates(); }

const loadingScreen = document.getElementById('loadingScreen');
if (siteSettings.showLoading === false || animationSettings.showLoadingAll === false) { loadingScreen.style.display = 'none'; }
else { loadingScreen.style.opacity = '0'; setTimeout(() => { loadingScreen.style.display = 'none'; }, 500); }
});

document.getElementById('uCurrency').addEventListener('change', function() { updatePlaceholderText(); });
</script>
</body>
</html>
