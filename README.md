<html lang="bn">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title id="pageTitle">Dollar Exchange - User Panel</title>
<link id="favicon" rel="icon" href="">
<style>
body{font-family: sans-serif;background:#f2f5f8;margin:0;color:#111;min-height:100vh}
#loadingScreen{position:fixed;top:0;left:0;right:0;bottom:0;background:#fff;display:flex;justify-content:center;align-items:center;flex-direction:column;z-index:99999;transition:opacity 0.5s ease}
.loader{width:50px;height:50px;border:5px solid #f3f3f3;border-top:5px solid #0b75ff;border-radius:50%;animation:spin 1s linear infinite}
@keyframes spin{0%{transform:rotate(0deg)}100%{transform:rotate(360deg)}}
.loading-text{margin-top:15px;color:#0b75ff;font-weight:bold}
.typing-text{display:inline-block;border-right:2px solid #fff;padding-right:5px;animation:blink-caret 0.75s step-end infinite}
@keyframes blink-caret{from,to{border-color:transparent}50%{border-color:#fff}}
.topbar{background:#fff;padding:10px 12px;display:flex;align-items:center;justify-content:space-between;box-shadow:0 2px 6px rgba(0,0,0,0.06);position:sticky;top:0;z-index:100}
.logo{display:flex;align-items:center;gap:10px}
.logo img{width:44px;height:44px;border-radius:8px;object-fit:cover}
.status-badge{padding:6px 12px;border-radius:8px;color:#fff;font-size:14px;font-weight:700}
.offline{background:#ef4444}
.online{background:#22c55e}
.top-buttons{display:flex;gap:8px}
.top-buttons button{padding:6px 12px;border-radius:20px;border:1px solid #0b75ff;background:#fff;color:#0b75ff;font-weight:700}
.blue-head{background:linear-gradient(180deg,#0037dd,#006bff);padding:36px 18px;text-align:center;border-bottom-left-radius:26px;border-bottom-right-radius:26px;color:#fff}
.blue-head h1{margin:0;font-size:26px;letter-spacing:0.2px}
.card{width:92%;max-width:720px;margin:14px auto;background:#fff;padding:14px;border-radius:10px;box-shadow:0 2px 10px rgba(0,0,0,0.06)}
input,select,button,textarea{width:100%;padding:10px;margin:8px 0;border-radius:8px;border:1px solid #ddd;font-size:15px;box-sizing:border-box}
button.primary{background:#0b75ff;color:#fff;border:none;padding:11px;border-radius:8px;cursor:pointer}
button.success{background:#16a34a;color:#fff;border:none;padding:11px;border-radius:8px;cursor:pointer}
button.danger{background:#ef4444;color:#fff;border:none;padding:11px;border-radius:8px;cursor:pointer}
.order-box{background:#fff;margin:10px;border-radius:10px;padding:12px;box-shadow:0 1px 6px rgba(0,0,0,0.06);display:flex;justify-content:space-between;align-items:center;gap:8px}
.order-info{flex:1}
.order-meta{min-width:110px;text-align:right}
.status{padding:6px 10px;border-radius:6px;color:#fff;font-weight:700}
.pending{background:#f59e0b}
.completed{background:#16a34a}
.rejected{background:#ef4444}
#nav{display:flex;justify-content:space-around;background:#111827;padding:12px;position:sticky;top:60px;z-index:99}
#nav button{width:48%;background:#22b573;color:#fff;border:none;padding:10px;border-radius:8px}
.wa-btn{position:fixed;bottom:22px;left:18px;background:#25d366;width:62px;height:62px;border-radius:50%;display:flex;justify-content:center;align-items:center;box-shadow:0 4px 12px rgba(0,0,0,0.18);z-index:90}
.wa-btn img{width:34px}
.small{font-size:13px;color:#666}
.modal{position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(0,0,0,0.5);display:flex;justify-content:center;align-items:center;padding:20px;z-index:1000;overflow:auto}
.modal .box{width:100%;max-width:520px;background:#fff;border-radius:12px;padding:16px;margin:auto;max-height:90vh;overflow-y:auto}
.id-badge{background:#f3f4f6;padding:8px;border-radius:8px;display:inline-block;width:100%;margin-bottom:6px;}
.order-empty{text-align:center;color:#6b7280;padding:26px}
.account-info{display:flex;gap:10px;align-items:center}
.btn-ghost{background:transparent;border:1px solid #0b75ff;color:#0b75ff;padding:8px 12px;border-radius:8px;cursor:pointer}
.maintenance-overlay{position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(255,255,255,0.95);z-index:9999;display:flex;justify-content:center;align-items:center;flex-direction:column;text-align:center;padding:20px}
.global-notification{position:fixed;top:70px;left:0;right:0;padding:10px;text-align:center;color:white;font-weight:bold;z-index:1000;display:none}
.notification-info{background-color:#31708f}
.trade-type-toggle{display:flex;background:#f1f5f9;border-radius:8px;overflow:hidden;margin:15px 0}
.trade-type-toggle button{flex:1;padding:12px;border:none;background:transparent;cursor:pointer;font-weight:600;transition:all 0.3s ease}
.trade-type-toggle button.active{background:#0b75ff;color:white}
.copy-btn-inside{background-color:#e5e7eb;border:none;padding:4px 10px;border-radius:4px;cursor:pointer;font-size:13px;transition:all 0.2s;float:right}
.copy-btn-inside.copied{background-color:#16a34a;color:white}

/* Telegram Connect Button Style */
.tg-connect-btn {
    background: #0088cc;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 8px;
    width: 100%;
    margin: 5px 0;
    cursor: pointer;
    font-weight: bold;
}
.tg-status-connected { color: #16a34a; font-size: 12px; }
.tg-status-not { color: #ef4444; font-size: 12px; }

@media (max-width:520px){.topbar{padding:8px}.blue-head{padding:24px 12px}.modal .box{margin:20px;width:calc(100% - 40px)}}
</style>
</head>
<body>

<div id="loadingScreen"><div class="loader"></div><div class="loading-text">লোড হচ্ছে...</div></div>
<div id="globalNotification" class="global-notification"></div>
<div id="maintenanceOverlay" class="maintenance-overlay" style="display:none;"><h2>Site Under Maintenance</h2><p id="maintenanceMessage"></p></div>

<!-- Account Modal -->
<div id="accountModal" class="modal" style="display:none;">
<div class="box" onclick="event.stopPropagation()">
<h3 id="accTitle">My Account</h3>
<div id="accForms">
<div id="loginForm">
<input id="loginEmail" placeholder="Email" type="email" />
<input id="loginPassword" placeholder="Password" type="password" />
<button class="primary" onclick="loginUser()">Login</button>
<div style="text-align:center;margin-top:8px">
<button class="btn-ghost" onclick="showSignup()">Sign Up</button>
<button class="btn-ghost" onclick="showForgotPassword()">Forget Password</button>
</div>
</div>

<div id="signupForm" style="display:none">
<input id="signupName" placeholder="আপনার নাম" />
<input id="signupEmail" placeholder="Email" type="email" />
<input id="signupNumber" placeholder="মোবাইল নম্বর" />
<input id="signupPassword" placeholder="Password" type="password" />
<button class="primary" onclick="signupUser()">Create Account</button>
<div style="text-align:center;margin-top:8px"><button class="btn-ghost" onclick="showLogin()">Already have account</button></div>
</div>

<div id="forgotPasswordForm" style="display:none">
<p style="margin-bottom:10px">Enter email to reset password:</p>
<input id="forgotEmail" placeholder="Email" type="email" />
<button class="primary" onclick="sendPasswordReset()">Send Code</button>
<div id="resetCodeSection" style="display:none;margin-top:10px">
<input id="resetCode" placeholder="Verification Code" />
<input id="resetNewPassword" placeholder="New Password" type="password" />
<button class="primary" onclick="resetPassword()">Reset Password</button>
</div>
<div style="text-align:center;margin-top:8px"><button class="btn-ghost" onclick="showLogin()">Back</button></div>
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
<div style="margin-top:12px">
    <!-- Telegram Connect Button in Profile -->
    <button id="tgConnectBtn" class="tg-connect-btn" onclick="openTelegramConnect()">🔗 Connect Telegram for Updates</button>
    <div id="tgStatus" style="text-align:center; margin-top:5px;"></div>
</div>
<div style="margin-top:12px;display:flex;gap:8px">
<button class="primary" onclick="closeAccountModal()">Close</button>
<button class="btn-ghost" onclick="logoutUser()">Logout</button>
</div>
</div>
</div>
</div>

<!-- TOP BAR -->
<div class="topbar">
<div class="logo">
<img id="logoImg" src="https://i.ibb.co.com/DD3h4qjv/file-000000007d947207b10fa3593fc67aa8.png" alt="Logo">
<div>
<div id="siteName" style="font-size:16px;font-weight:800;color:#0037dd">Fast & Secure Exchange</div>
<div id="siteTagline" class="small">সকাল৯ঃ০০টা থেকে রাত১০ঃ০০টা</div>
</div>
</div>
<div id="opStatus" class="status-badge offline">Offline</div>
<div class="top-buttons">
<button id="myAccountBtn" onclick="openAccountModal()">My Account</button>
</div>
</div>

<div class="blue-head">
<h1 id="welcomeTitle">Welcome to Dollar Exchange</h1>
<p id="welcomeSubtitle" class="small">দয়া করে ট্রানজেকশন শুরু করার আগে নিয়মগুলো পড়ে নিন</p>
</div>

<div id="nav">
<button id="navButton" onclick="showUser()">নগদ বিকাশ 5 টাকা সেন্ড মানি ফি কেটে নেওয়া হয়</button>
</div>

<!-- USER AREA -->
<div id="userArea">
<div class="card">
<div class="trade-type-toggle">
<button id="bhaiButton" class="active" onclick="setTradeType('buy')">buy</button>
<button id="saleButton" onclick="setTradeType('sell')">sell</button>
</div>
<input id="uName" placeholder="আপনার নাম" />
<select id="uCurrency" onchange="updatePlaceholderText()"></select>
<input id="uDollar" type="number" placeholder="কত ডলার সেল দিবেন" oninput="calc()" />
<input id="uTaka" placeholder="টাকায় মূল্য" readonly />
<div id="feeInfo" style="margin:8px 0; font-size:13px; color:#666; display:none;"></div>
<select id="uPayment"></select>
<input id="uNumber" placeholder="আপনার পেমেন্ট নাম্বার" />
<select id="uVia">
<option value="bKash">bKash</option>
<option value="Nagad">Nagad</option>
<option value="Rocket">Rocket</option>
</select>
<input id="uTx" placeholder="এই অপশনে কিছু লিখতে হবে না)">
<button class="primary" onclick="placeOrder()">অর্ডার দিন</button>
</div>

<h3 style="text-align:center;margin-top:8px">📦 আপনার অর্ডারসমূহ</h3>
<div id="myOrdersContainer" class="card" style="padding:8px;">
<div id="myOrders"></div>
</div>
</div>

<!-- ORDER MODALS -->
<div id="modal" style="display:none;"><div class="modal" onclick="closeModal(event)"><div class="box" onclick="event.stopPropagation()"><h3 id="mTitle">Order Details</h3><div id="mBody"></div><div style="margin-top:10px;display:flex;gap:8px"><input id="mTx" placeholder="ট্রানজেকশন আইডি দিন"><button class="primary" onclick="saveTx()">সংরক্ষণ</button></div><div style="margin-top:12px;text-align:right"><button onclick="closeModal()">Close</button></div></div></div></div>
<div id="confirmModal" style="display:none;"><div class="modal" onclick="closeConfirm(event)"><div class="box" onclick="event.stopPropagation()"><h3>Confirm Your Order</h3><div id="cBody"></div><input id="cTx" placeholder="আপনার Transaction ID লিখুন" /><button class="primary" onclick="confirmOrder()">Confirm Order</button><div style="margin-top:12px;text-align:right"><button onclick="closeConfirm()">Close</button></div></div></div></div>
<a id="whatsappLink" href="https://wa.me/qr/DTBEJ472LPKOA1" class="wa-btn" target="_blank"><img src="https://i.ibb.co/dnLD0Wf/20251129-064417.jpg" alt="wa"></a>

<script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore-compat.js"></script>
<script>
// CONFIG
const TELEGRAM_BOT_TOKEN = "8352210003:AAHVyrRGz7aePhikEn8B72fFNARQhfiMbyI";
const TELEGRAM_CHAT_ID = "7427334644";
const firebaseConfig = {
apiKey: "AIzaSyCE57xIZr1igoPT7EkpDz0SIVYvFHle97U",
authDomain: "dollar-exchange-bdt-fa179.firebaseapp.com",
projectId: "dollar-exchange-bdt-fa179",
storageBucket: "dollar-exchange-bdt-fa179.firebasestorage.app",
messagingSenderId: "294819905234",
appId: "1:294819905234:web:4da06ee71d54daeb40770b"
};
firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

const modal = document.getElementById('modal');
const confirmModal = document.getElementById('confirmModal');
const accountModal = document.getElementById('accountModal');

let currencies = [
{ id: 'Payeer', name: 'Payeer', buyRate: 68, sellRate: 70, paymentId: 'P1131698605', minDollar: 5, maxDollar: 500 },
{ id: 'Binance', name: 'Binance', buyRate: 19, sellRate: 20, paymentId: '1188473082', minDollar: 1, maxDollar: 1000 },
{ id: 'Advcash', name: 'Advcash', buyRate: 58, sellRate: 60, paymentId: 'U 1048 5654 4714', minDollar: 10, maxDollar: 300 }
];
let paymentMethods = [];
let siteSettings = { name: 'Fast & Secure Exchange', tagline: 'সকাল৯ঃ০০টা থেকে রাত১০ঃ০০টা', primaryColor: '#0b75ff', secondaryColor: '#0037dd', backgroundColor: '#f2f5f8', workStartTime: '09:00', workEndTime: '22:00', statusOverride: '', orderInstructions: '', whatsappLink: 'https://wa.me/qr/DTBEJ472LPKOA1', minDollarAmount: 1, maxDollarAmount: 1000, transactionFee: 0, transactionFeePercent: 0, logoUrl: 'https://i.ibb.co.com/DD3h4qjv/file-000000007d947207b10fa3593fc67aa8.png', maintenanceMode: false, maintenanceMessage: '', requireLogin: false, showLoading: true };
let contentSettings = { welcomeTitle: 'Welcome to Dollar Exchange', welcomeSubtitle: 'দয়া করে ট্রানজেকশন শুরু করার আগে নিয়মগুলো পড়ে নিন', navButtonText: 'নগদ বিকাশ 5 টাকা সেন্ড মানি ফি কেটে নেওয়া হয়', globalNotification: '', notificationType: 'info', notificationActive: false, typingText: '', typingSpeed: 80 };
let currentTradeType = 'bhai';

// --- TELEGRAM FUNCTIONS ---
async function sendTelegramNotification(orderDetails) {
    const message = `
🔔 *New Order!*
👤 Name: ${orderDetails.name}
📱 Phone: ${orderDetails.number}
💵 Amount: ${orderDetails.dollar}$ = ${orderDetails.taka} Tk
📦 Currency: ${orderDetails.currency}
    `;
    await fetch(`https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ chat_id: TELEGRAM_CHAT_ID, text: message, parse_mode: "Markdown" })
    });
}

// Connect Telegram
function openTelegramConnect() {
    // ইউজারকে বটের লিংকে পাঠানো হচ্ছে একটি কোড সহ
    const current = getCurrentUser();
    if(!current) return;
    
    // একটি ইউনিক কোড তৈরি করা হলো (এটি আসলে ইউজারের একাউন্ট আইডি বা র‍্যান্ডম নাম্বার হতে পারে)
    // আমরা সহজ সমাধান করছি: ইউজারকে বটে স্টার্ট দিতে বলব এবং তারপর একটি কোড বসাতে বলব।
    
    // পদ্ধতি: ইউজারকে বটে স্টার্ট দিতে হবে। বট তাকে একটি ID দেব। সেই ID ওয়েবসাইটে বসাতে হবে।
    // যেহেতু আমাদের বট সার্ভার নেই, আমরা ইউজারকে তার Chat ID বের করে দিতে পারি একটি টুল দিয়ে।
    
    alert("Telegram এ আমাদের বটে যান এবং Start চাপুন। তারপর আপনার Chat ID টি আমাদের দিন।\n\nBot Link: t.me/YOUR_BOT_USERNAME");
    
    // সহজ সমাধান: ইউজার যদি username দেয়, আমরা সেটা ব্যবহার করব। 
    // কিন্তু Auto Message এর জন্য Chat ID লাগে।
    // তাই ইউজারকে একটি ভেরিফিকেশন কোড দিতে হবে।
    
    const code = "CONNECT_" + Math.random().toString(36).substring(7);
    localStorage.setItem('tg_connect_code', code);
    
    // ইউজারকে টেলিগ্রামে পাঠানো হলো এই কোড সহ
    // এটি একটি Deep Linking উদাহরণ
    window.open(`https://t.me/YOUR_BOT_USERNAME?start=${code}`, '_blank');
}

// Save Chat ID (This would typically be done via backend, but here is the frontend logic to receive it)
async function checkTelegramVerification() {
    // চেক করা হচ্ছে URL এ কোনো টেলিগ্রাম আইডি এসেছে কিনা (যদি বট রিডাইরেক্ট করে)
    const urlParams = new URLSearchParams(window.location.search);
    const chatId = urlParams.get('tg_id');
    if(chatId) {
        const current = getCurrentUser();
        if(current) {
            await db.collection('users').where('email', '==', current.email).get().then(snapshot => {
                if(!snapshot.empty) snapshot.docs[0].ref.update({ telegramChatId: chatId });
            });
            alert("Telegram Connected Successfully!");
            updateAccountUI();
        }
    }
}


// --- ACCOUNT FUNCTIONS ---
function openAccountModal(){ accountModal.style.display = "flex"; document.body.classList.add('modal-open'); updateAccountUI(); }
function closeAccountModal(){ accountModal.style.display = "none"; document.body.classList.remove('modal-open'); }
function showSignup(){ loginForm.style.display='none'; signupForm.style.display='block'; forgotPasswordForm.style.display='none'; accProfile.style.display='none'; accTitle.innerText = 'Sign Up'; }
function showLogin(){ loginForm.style.display='block'; signupForm.style.display='none'; forgotPasswordForm.style.display='none'; accProfile.style.display='none'; accTitle.innerText = 'Login'; }
function showForgotPassword(){ loginForm.style.display='none'; signupForm.style.display='none'; forgotPasswordForm.style.display='block'; accProfile.style.display='none'; accTitle.innerText = 'Reset Password'; }

async function signupUser(){
const name = signupName.value.trim();
const email = signupEmail.value.trim().toLowerCase();
const number = signupNumber.value.trim();
const pass = signupPassword.value;
if(!name || !email || !pass || !number){ alert('সব ঘর পূরণ করুন'); return; }
try {
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (!userSnapshot.empty) { alert('এই ইমেইল দিয়ে আগে থেকেই অ্যাকাউন্ট আছে'); return; }
await db.collection('users').add({ name, email, number, password: pass, userType: 'regular', createdAt: new Date().toISOString() });
localStorage.setItem('currentUser', JSON.stringify({ name, email, number, userType: 'regular' }));
signupName.value=''; signupEmail.value=''; signupNumber.value=''; signupPassword.value='';
updateAccountUI(); closeAccountModal(); alert('Account created ✔'); prefillUserFields(); loadMyOrders();
} catch (error) { console.error(error); alert("Error creating account."); }
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
} catch (error) { console.error(error); alert("Error logging in."); }
}

function logoutUser(){ localStorage.removeItem('currentUser'); updateAccountUI(); alert('Logged out'); uName.value=''; uNumber.value=''; loadMyOrders(); }
function getCurrentUser(){ return JSON.parse(localStorage.getItem('currentUser')||'null'); }

function updateAccountUI(){
const u = getCurrentUser();
if(u){
accProfile.style.display='block'; loginForm.style.display='none'; signupForm.style.display='none'; forgotPasswordForm.style.display='none'; accTitle.innerText = 'Account';
pName.innerText = u.name; pEmail.innerText = u.email; pNumber.innerText = u.number;
myAccountBtn.innerText = 'Account ✓';
} else {
accProfile.style.display='none'; loginForm.style.display='block'; signupForm.style.display='none'; forgotPasswordForm.style.display='none'; accTitle.innerText = 'Login'; myAccountBtn.innerText = 'My Account';
}
}

function prefillUserFields(){
const u = getCurrentUser();
if(u){ uName.value = u.name || ''; uNumber.value = u.number || ''; }
}

async function sendPasswordReset() {
const email = forgotEmail.value.trim().toLowerCase();
if (!email) { alert('Please enter email'); return; }
try {
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (userSnapshot.empty) { alert('No account found'); return; }
const resetCode = Math.floor(100000 + Math.random() * 900000).toString();
const expiryTime = new Date(Date.now() + 3600000).toISOString();
await db.collection('passwordResets').add({ email, resetCode, expiryTime, used: false });
document.getElementById('resetCodeSection').style.display = 'block';
alert(`Demo Code: ${resetCode}`);
} catch (error) { console.error(error); alert("Error sending reset."); }
}

async function resetPassword() {
const email = forgotEmail.value.trim().toLowerCase();
const code = resetCode.value.trim();
const newPassword = resetNewPassword.value;
if (!email || !code || !newPassword) { alert('Fill all fields'); return; }
try {
const resetSnapshot = await db.collection('passwordResets').where('email', '==', email).where('resetCode', '==', code).where('used', '==', false).get();
if (resetSnapshot.empty) { alert('Invalid code'); return; }
const resetDoc = resetSnapshot.docs[0];
if (new Date() > new Date(resetDoc.data().expiryTime)) { alert('Code expired'); return; }
await db.collection('passwordResets').doc(resetDoc.id).update({ used: true });
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (!userSnapshot.empty) { await db.collection('users').doc(userSnapshot.docs[0].id).update({ password: newPassword }); }
forgotEmail.value = ''; resetCode.value = ''; resetNewPassword.value = '';
document.getElementById('resetCodeSection').style.display = 'none';
alert('Password reset successful!'); showLogin();
} catch (error) { console.error(error); alert("Error resetting password."); }
}

// --- CORE LOGIC ---
async function loadSiteSettings() { try { const doc = await db.collection('settings').doc('site').get(); if (doc.exists) siteSettings = { ...siteSettings, ...doc.data() }; applySiteSettings(); } catch (e) { console.error(e); } }
async function loadContentSettings() { try { const doc = await db.collection('settings').doc('content').get(); if (doc.exists) contentSettings = { ...contentSettings, ...doc.data() }; applyContentSettings(); } catch (e) { console.error(e); } }
async function loadPaymentMethods() { try { const doc = await db.collection('settings').doc('paymentMethods').get(); if (doc.exists) paymentMethods = doc.data().list || []; updatePaymentMethods(); } catch (e) { console.error(e); } }

function applySiteSettings() {
document.title = siteSettings.name || 'Dollar Exchange';
document.getElementById('pageTitle').textContent = siteSettings.name || 'Dollar Exchange';
if (siteSettings.logoUrl) document.getElementById('logoImg').src = siteSettings.logoUrl;
document.getElementById('siteName').textContent = siteSettings.name;
document.getElementById('siteTagline').textContent = `সকাল ${siteSettings.workStartTime || '09:00'} টা থেকে রাত ${siteSettings.workEndTime || '22:00'} টা`;
document.querySelector('.blue-head').style.background = `linear-gradient(180deg,${siteSettings.secondaryColor},${siteSettings.primaryColor})`;
if (siteSettings.whatsappLink) document.getElementById('whatsappLink').href = siteSettings.whatsappLink;
if (siteSettings.maintenanceMode) { document.getElementById('maintenanceOverlay').style.display = 'flex'; document.getElementById('maintenanceMessage').textContent = siteSettings.maintenanceMessage; }
}
function applyContentSettings() {
document.getElementById('welcomeTitle').textContent = contentSettings.welcomeTitle;
document.getElementById('welcomeSubtitle').textContent = contentSettings.welcomeSubtitle;
document.getElementById('navButton').textContent = contentSettings.navButtonText;
if (contentSettings.globalNotification && contentSettings.notificationActive) { const n = document.getElementById('globalNotification'); n.textContent = contentSettings.globalNotification; n.className = `global-notification notification-${contentSettings.notificationType}`; n.style.display = 'block'; }
}
function updatePaymentMethods() { const el = document.getElementById('uPayment'); el.innerHTML = ''; paymentMethods.forEach(m => { const o = document.createElement('option'); o.value = m.id; o.textContent = m.name; el.appendChild(o); }); }

async function loadCurrencies(){
try {
const doc = await db.collection('settings').doc('currencies').get();
if (doc.exists) currencies = doc.data().list || currencies;
} catch (e) { console.error(e); }
const uCurrency = document.getElementById('uCurrency');
uCurrency.innerHTML = '';
currencies.forEach(currency => {
const option = document.createElement('option');
option.value = currency.id;
const rate = currentTradeType === 'bhai' ? currency.buyRate : currency.sellRate;
option.textContent = `${currency.name} (${rate} BDT)`;
uCurrency.appendChild(option);
});
if (uDollar.value) calc();
}

function setTradeType(type) {
currentTradeType = type;
document.getElementById('bhaiButton').classList.toggle('active', type === 'bhai');
document.getElementById('saleButton').classList.toggle('active', type === 'sale');
loadCurrencies();
}

function calc(){
const dollar = Number(uDollar.value) || 0;
const currency = currencies.find(c => c.id === uCurrency.value);
const rate = currency ? (currentTradeType === 'bhai' ? currency.buyRate : currency.sellRate) : 0;
uTaka.value = (dollar * rate).toFixed(2);
}

function updatePlaceholderText() {
const currency = currencies.find(c => c.id === uCurrency.value);
calc();
if (currency) uDollar.placeholder = `কত ডলার (${currency.minDollar} থেকে ${currency.maxDollar})`;
}

function placeOrder(){
const current = getCurrentUser();
if(siteSettings.requireLogin && !current){ alert('Login required'); openAccountModal(); return; }
const name = (uName.value.trim() || current?.name);
const number = (uNumber.value.trim() || current?.number);
const currencyId = uCurrency.value;
const currency = currencies.find(c => c.id === currencyId);
const dollar = parseFloat(uDollar.value);
const taka = uTaka.value;
const payment = uPayment.value;
const via = uVia.value || "";
const tx = uTx.value.trim() || "";

if(!name || !number || !dollar){ alert('সব ঘর পূরণ করুন'); return; }

window.tempOrder = { name, number, currency: currency.name, currencyId, dollar, taka, payment, via, tx, tradeType: currentTradeType };
const paymentIds = currencies.map(c => `<div class="id-badge">${c.name} ID: ${c.paymentId}<button class="copy-btn-inside" onclick="copyText('${c.paymentId}', this)">Copy</button></div>`).join('');
cBody.innerHTML = `<div>নাম: <b>${name}</b></div><div>নম্বার: <b>${number}</b></div><div>কারেন্সি: <b>${currency.name}</b></div><div>ডলার: <b>${dollar}</b> → টাকা: <b>${taka}</b></div><div style="margin-top:10px">পেমেন্ট পাঠানোর আইডি:</div>${paymentIds}`;
cTx.value = tx;
confirmModal.style.display = "flex"; document.body.classList.add('modal-open');
}

async function confirmOrder(){
const tx = cTx.value.trim();
const o = tempOrder;
if(!o) return;
try {
const current = getCurrentUser();
const newOrder = {
name: o.name, number: o.number, currency: o.currency, currencyId: o.currencyId, dollar: o.dollar, taka: o.taka, paymentMethod: o.payment, via: o.via || "", trx: tx || "",
status: 'PENDING', createdAt: new Date().toISOString(), userEmail: current ? current.email : null, userType: current ? current.userType || 'regular' : 'regular', tradeType: o.tradeType || 'sell'
};
const docRef = await db.collection('orders').add(newOrder);
newOrder.id = docRef.id;
sendTelegramNotification(newOrder);
confirmModal.style.display="none"; document.body.classList.remove('modal-open'); tempOrder=null;
loadMyOrders(); alert("অর্ডার Confirm হয়েছে ✔");
uDollar.value=""; uTaka.value=""; uTx.value=""; uVia.value="";
} catch (error) { console.error(error); alert("Error creating order."); }
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
let orders = [];
if(current){
const snap = await db.collection('orders').where('userEmail', '==', current.email).get();
snap.forEach(doc => orders.push({id: doc.id, ...doc.data()}));
} else {
const number = uNumber.value.trim();
if(number) {
const snap = await db.collection('orders').where('number', '==', number).get();
snap.forEach(doc => orders.push({id: doc.id, ...doc.data()}));
}
}
orders.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
renderOrders(orders);
} catch (error) { console.error(error); myOrders.innerHTML='<div class="order-empty">Error</div>'; }
}

function renderOrders(orders) {
if(orders.length===0){ myOrders.innerHTML='<div class="order-empty">আপনার অর্ডার নেই</div>'; return; }
orders.forEach(o=>{
const s = getBanglaStatus(o.status);
myOrders.innerHTML += `
<div class="order-box">
<div class="order-info">
<div><b>${o.name}</b> <span class="small">• ${new Date(o.createdAt).toLocaleString()}</span></div>
<div class="small">${o.currency} • ${o.dollar}$ → ${o.taka} TK</div>
</div>
<div class="order-meta">
<span class="status ${s.cls}">${s.text}</span>
<button onclick="openModal('${o.id}')">View</button>
</div>
</div>`;
});
}

async function openModal(id){
currentModalId=id;
const doc = await db.collection('orders').doc(id).get();
if (!doc.exists) return;
const o = doc.data();
mTitle.innerText="Order — "+o.name;
mBody.innerHTML=`<div>Amount: <b>${o.dollar}$</b></div><div>Status: <b>${o.status}</b></div><div>TXID: ${o.trx || 'N/A'}</div>`;
mTx.value = o.trx || "";
modal.style.display="flex"; document.body.classList.add('modal-open');
}

function closeModal(event){ if (!event || event.target === modal || event.target.textContent === 'Close') { modal.style.display='none'; document.body.classList.remove('modal-open'); currentModalId=null; } }
function closeConfirm(event){ if (!event || event.target === confirmModal || event.target.textContent === 'Close') { confirmModal.style.display='none'; document.body.classList.remove('modal-open'); } }

async function saveTx(){
if(!currentModalId) return;
await db.collection('orders').doc(currentModalId).update({ trx: mTx.value.trim() });
loadMyOrders(); alert("TXID Updated"); closeModal();
}

function copyText(text, btn) { navigator.clipboard.writeText(text).then(() => { btn.innerText = "Copied!"; btn.classList.add('copied'); setTimeout(() => { btn.innerText = "Copy"; btn.classList.remove('copied'); }, 1500); }); }

function updateStatus(){
let isOnline = false;
const current = new Date();
if (siteSettings.statusOverride === 'online') isOnline = true;
else if (siteSettings.statusOverride === 'offline') isOnline = false;
else {
const h = current.getHours();
isOnline = h >= 9 && h < 22;
}
if(isOnline){ opStatus.innerText='Online'; opStatus.className='status-badge online'; }
else { opStatus.innerText='Offline'; opStatus.className='status-badge offline'; }
}
function showUser(){ userArea.style.display='block'; }

window.addEventListener('load',async()=>{
await loadSiteSettings();
await loadContentSettings();
await loadPaymentMethods();
await loadCurrencies();
updateAccountUI();
prefillUserFields();
loadMyOrders();
updatePlaceholderText();
updateStatus();
checkTelegramVerification(); // Check if returning from Telegram

const loadingScreen = document.getElementById('loadingScreen');
if (siteSettings.showLoading === false) loadingScreen.style.display = 'none';
else { loadingScreen.style.opacity = '0'; setTimeout(() => loadingScreen.style.display = 'none', 500); }
});
document.getElementById('uCurrency').addEventListener('change', updatePlaceholderText);
</script>
</body>
</html>
