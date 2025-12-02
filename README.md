<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Dollar Exchange - Updated</title>
<style>
body{font-family: sans-serif;background:#f2f5f8;margin:0;color:#111}
.topbar{background:#fff;padding:10px 12px;display:flex;align-items:center;justify-content:space-between;box-shadow:0 2px 6px rgba(0,0,0,0.06)}
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

input,select,button,textarea{width:100%;padding:10px;margin:8px 0;border-radius:8px;border:1px solid #ddd;font-size:15px}
button.primary{background:#0b75ff;color:#fff;border:none;padding:11px;border-radius:8px;cursor:pointer}

.order-box{background:#fff;margin:10px;border-radius:10px;padding:12px;box-shadow:0 1px 6px rgba(0,0,0,0.06);display:flex;justify-content:space-between;align-items:center;gap:8px}
.order-info{flex:1}
.order-meta{min-width:110px;text-align:right}
.status{padding:6px 10px;border-radius:6px;color:#fff;font-weight:700}
.pending{background:#f59e0b}
.completed{background:#16a34a}
.rejected{background:#ef4444}

#nav{display:flex;justify-content:space-around;background:#111827;padding:12px}
#nav button{width:48%;background:#22b573;color:#fff;border:none;padding:10px;border-radius:8px}

.wa-btn{position:fixed;bottom:22px;left:18px;background:#25d366;width:62px;height:62px;border-radius:50%;display:flex;justify-content:center;align-items:center;box-shadow:0 4px 12px rgba(0,0,0,0.18)}
.wa-btn img{width:34px}

.small{font-size:13px;color:#666}
.modal{position:fixed;inset:0;background:rgba(0,0,0,0.5);display:flex;justify-content:center;align-items:flex-end;padding:20px;z-index:999}
.modal .box{width:100%;max-width:520px;background:#fff;border-radius:12px;padding:16px}

.id-badge{background:#f3f4f6;padding:8px;border-radius:8px;display:inline-block;width:100%}
.order-empty{text-align:center;color:#6b7280;padding:26px}

.account-info{display:flex;gap:10px;align-items:center}
.btn-ghost{background:transparent;border:1px solid #0b75ff;color:#0b75ff;padding:8px 12px;border-radius:8px;cursor:pointer}

.control-row{display:flex;gap:10px}
.control-row > *{flex:1}

@media (max-width:520px){
.topbar{padding:8px}
.blue-head{padding:24px 12px}
}
</style>
</head>
<body>

<!-- Admin Login (hidden) -->
<div id="adminLogin" class="modal" style="display:none;">
<div class="box">
<h3>Admin Login</h3>
<input id="adminPass" type="password" placeholder="Enter Password">
<button class="primary" onclick="checkAdmin()">Login</button>
<div style="text-align:right;margin-top:8px"><button onclick="adminLogin.style.display='none'">Close</button></div>
</div>
</div>

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
<button class="btn-ghost" onclick="showFisher()">Fisher</button>
<button class="btn-ghost" onclick="showForgotPassword()">Forget Password</button>
</div>
</div>

<div id="signupForm" style="display:none">
<input id="signupName" placeholder="আপনার নাম" />
<input id="signupEmail" placeholder="Email" type="email" />
<input id="signupNumber" placeholder="মোবাইল নম্বর" />
<input id="signupPassword" placeholder="Password" type="password" />
<button class="primary" onclick="signupUser()">Create Account</button>
<div style="text-align:center;margin-top:8px">
<button class="btn-ghost" onclick="showLogin()">Already have account</button>
</div>
</div>

<div id="fisherForm" style="display:none">
<input id="fisherName" placeholder="আপনার নাম" />
<input id="fisherEmail" placeholder="Email" type="email" />
<input id="fisherNumber" placeholder="মোবাইল নম্বর" />
<input id="fisherPassword" placeholder="Password" type="password" />
<button class="primary" onclick="signupFisher()">Create Fisher Account</button>
<div style="text-align:center;margin-top:8px">
<button class="btn-ghost" onclick="showLogin()">Already have account</button>
</div>
</div>

<div id="forgotPasswordForm" style="display:none">
<p style="margin-bottom:10px">Enter your email address to reset your password:</p>
<input id="forgotEmail" placeholder="Email" type="email" />
<button class="primary" onclick="sendPasswordReset()">Send Reset Code</button>
<div id="resetCodeSection" style="display:none;margin-top:10px">
<p style="margin-bottom:10px">Enter the verification code sent to your email:</p>
<input id="resetCode" placeholder="Verification Code" />
<input id="newPassword" placeholder="New Password" type="password" />
<button class="primary" onclick="resetPassword()">Reset Password</button>
</div>
<div style="text-align:center;margin-top:8px">
<button class="btn-ghost" onclick="showLogin()">Back to Login</button>
</div>
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
<img src="https://i.ibb.co/5WWPvnQj/20251128-160723.png" alt="logo">
<div>
<div style="font-size:16px;font-weight:800;color:#0037dd">dollar bay sall</div>
<div class="small">Fast & Secure Exchange</div>
</div>
</div>

<div id="opStatus" class="status-badge offline">Offline</div>

<div class="top-buttons">
<button id="myAccountBtn" onclick="openAccountModal()">My Account</button>
</div>
</div>

<div class="blue-head">
<h1>Welcome to Dollar Exchange</h1>
<p class="small">দয়া করে ট্রানজেকশন শুরু করার আগে নিয়মগুলো পড়ে নিন</p>
</div>

<div id="nav">
<button onclick="showUser()">নগদ বিকাশ 5 টাকা সেন্ড মানি ফি কেটে নেওয়া হয়</button>
</div>

<!-- USER AREA -->
<div id="userArea">
<h2 style="text-align:center;margin-top:18px"></h2>

<div class="card">
<input id="uName" placeholder="আপনার নাম" />
<select id="uCurrency" onchange="calc()">
<option value="Payeer">Payeer</option>
<option value="Binance">Binance</option>
<option value="gmail farmer">Binance</option>
</select>

<input id="uDollar" type="number" placeholder="কত ডলার সেল দিবেন" oninput="calc()" />
<input id="uTaka" placeholder="টাকায় মূল্য" readonly />

<select id="uPayment">
<option value="bKash">sand money </option>
<option value="Nagad">cash out </option>
</select>

<input id="uNumber" placeholder="আপনার পেমেন্ট নম্বর" />

<!-- NEW: মাধ্যম (via) এবং TX ইনপুট (Optional - ইউজার যদি TX দিতে চায়) -->
<select id="uVia">
<option value="">-- মাধ্যমে পেমেন্ট --</option>
<option value="bKash">bKash</option>
<option value="Nagad">Nagad</option>
</select>

<input id="uTx" placeholder="এই অপশনে কিছু লিখতে হবে না)">

<button class="primary" onclick="placeOrder()">অর্ডার দিন</button>
</div>

<h3 style="text-align:center;margin-top:8px">📦 আপনার অর্ডারসমূহ</h3>
<div id="myOrdersContainer" class="card" style="padding:8px;">
<div id="myOrders"></div>
</div>
</div>

<!-- ADMIN AREA -->
<div id="adminArea" style="display:none;">
<h2 style="text-align:center;margin-top:18px">🛠 Admin Panel</h2>

<div class="card">
<h3>💱 Dollar Rate Control</h3>

<label>Payeer Rate (1 USD = ? Tk)</label>
<input id="ratePayeer" type="number"/>

<label>Binance Rate (1 USD = ? Tk)</label>
<input id="rateBinance" type="number"/>

<button class="primary" onclick="saveRates()">💾 Save Rates</button>
</div>

<div class="card">
<div style="margin-bottom:10px"><b>Search by user number:</b>
<input id="adminSearch" placeholder="phone number" oninput="loadAdmin()" />
</div>
<div id="adminOrders"></div>
</div>
</div>

<!-- ORDER DETAILS MODAL -->
<div id="modal" style="display:none;">
<div class="modal" onclick="closeModal(event)">
<div class="box" onclick="event.stopPropagation()">
<h3 id="mTitle">Order Details</h3>
<div id="mBody"></div>

<div style="margin-top:10px;display:flex;gap:8px">
<input id="mTx" placeholder="ট্রানজেকশন আইডি দিন">
<button class="primary" onclick="saveTx()">সংরক্ষণ</button>
</div>

<div style="margin-top:12px;text-align:right"><button onclick="closeModal()">Close</button></div>
</div>
</div>
</div>

<!-- CONFIRM ORDER MODAL -->
<div id="confirmModal" style="display:none;">
<div class="modal" onclick="closeConfirm(event)">
<div class="box" onclick="event.stopPropagation()">
<h3>Confirm Your Order</h3>

<div id="cBody"></div>

<input id="cTx" placeholder="আপনার Transaction ID লিখুন" />

<button class="primary" onclick="confirmOrder()">Confirm Order</button>

<div style="margin-top:12px;text-align:right"><button onclick="closeConfirm()">Close</button></div>
</div>
</div>
</div>

<!-- WhatsApp Button -->
<a href="https://wa.me/qr/DTBEJ472LPKOA1" class="wa-btn" target="_blank">
<img src="https://i.ibb.co/dnLD0Wf/20251129-064417.jpg" alt="wa">
</a>

<!-- Firebase SDK -->
<script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore-compat.js"></script>
<script>
// Firebase Config
const firebaseConfig = {
apiKey: "AIzaSyBUMQNzDO6cRdRHFPYOGOBfApzuaidkw2E",
authDomain: "dollar-exchange-bdt.firebaseapp.com",
projectId: "dollar-exchange-bdt",
storageBucket: "dollar-exchange-bdt.firebasestorage.app",
messagingSenderId: "666904772438",
appId: "1:666904772438:web:860c9207c1a1e59a2820f7"
};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

// Get DOM elements
const modal = document.getElementById('modal');
const confirmModal = document.getElementById('confirmModal');
const accountModal = document.getElementById('accountModal');
const adminLogin = document.getElementById('adminLogin');

// Payment IDs
const PAYEER_ID = 'P1131698605';
const BINANCE_ID = '1188473082';

// DEFAULT RATES
let rates = {
Payeer: 70,
Binance: 20
};

// ACCOUNT
function openAccountModal(){ accountModal.style.display = "flex"; updateAccountUI(); }
function closeAccountModal(){ accountModal.style.display = "none"; }
function showSignup(){ loginForm.style.display='none'; signupForm.style.display='block'; fisherForm.style.display='none'; forgotPasswordForm.style.display='none'; accProfile.style.display='none'; accTitle.innerText = 'Sign Up'; }
function showLogin(){ loginForm.style.display='block'; signupForm.style.display='none'; fisherForm.style.display='none'; forgotPasswordForm.style.display='none'; accProfile.style.display='none'; accTitle.innerText = 'Login'; }
function showFisher(){ loginForm.style.display='none'; signupForm.style.display='none'; fisherForm.style.display='block'; forgotPasswordForm.style.display='none'; accProfile.style.display='none'; accTitle.innerText = 'Fisher Sign Up'; }
function showForgotPassword(){ loginForm.style.display='none'; signupForm.style.display='none'; fisherForm.style.display='none'; forgotPasswordForm.style.display='block'; accProfile.style.display='none'; accTitle.innerText = 'Reset Password'; }

async function signupUser(){
const name = signupName.value.trim();
const email = signupEmail.value.trim().toLowerCase();
const number = signupNumber.value.trim();
const pass = signupPassword.value;

if(!name || !email || !pass || !number){ 
alert('সব ঘর পূরণ করুন'); 
return; 
}

try {
// Check if user already exists
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (!userSnapshot.empty) {
alert('এই ইমেইল দিয়ে আগে থেকেই অ্যাকাউন্ট আছে');
return;
}

// Create new user
await db.collection('users').add({
name,
email,
number,
password: pass,
userType: 'regular',
createdAt: new Date().toISOString()
});

// Set current user in localStorage for session
localStorage.setItem('currentUser', JSON.stringify({ name, email, number, userType: 'regular' }));

signupName.value=''; 
signupEmail.value=''; 
signupNumber.value=''; 
signupPassword.value='';

updateAccountUI(); 
closeAccountModal(); 
alert('Account created and logged in ✔'); 
prefillUserFields(); 
loadMyOrders();
} catch (error) {
console.error("Error creating user:", error);
alert("Error creating account. Please try again.");
}
}

async function signupFisher(){
const name = fisherName.value.trim();
const email = fisherEmail.value.trim().toLowerCase();
const number = fisherNumber.value.trim();
const pass = fisherPassword.value;

if(!name || !email || !pass || !number){ 
alert('সব ঘর পূরণ করুন'); 
return; 
}

try {
// Check if user already exists
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (!userSnapshot.empty) {
alert('এই ইমেইল দিয়ে আগে থেকেই অ্যাকাউন্ট আছে');
return;
}

// Create new user
await db.collection('users').add({
name,
email,
number,
password: pass,
userType: 'fisher',
createdAt: new Date().toISOString()
});

// Set current user in localStorage for session
localStorage.setItem('currentUser', JSON.stringify({ name, email, number, userType: 'fisher' }));

fisherName.value=''; 
fisherEmail.value=''; 
fisherNumber.value=''; 
fisherPassword.value='';

updateAccountUI(); 
closeAccountModal(); 
alert('Fisher Account created and logged in ✔'); 
prefillUserFields(); 
loadMyOrders();
} catch (error) {
console.error("Error creating fisher account:", error);
alert("Error creating fisher account. Please try again.");
}
}

async function loginUser(){
const email = loginEmail.value.trim().toLowerCase();
const pass = loginPassword.value;

try {
const userSnapshot = await db.collection('users').where('email', '==', email).where('password', '==', pass).get();

if (userSnapshot.empty) {
alert('Invalid credentials');
return;
}

const user = userSnapshot.docs[0].data();
localStorage.setItem('currentUser', JSON.stringify({ 
name: user.name, 
email: user.email, 
number: user.number,
userType: user.userType || 'regular'
}));

updateAccountUI(); 
closeAccountModal(); 
alert('Login successful ✔'); 
prefillUserFields(); 
loadMyOrders();
} catch (error) {
console.error("Error logging in:", error);
alert("Error logging in. Please try again.");
}
}

function logoutUser(){ 
localStorage.removeItem('currentUser'); 
updateAccountUI(); 
alert('Logged out'); 
uName.value=''; 
uNumber.value=''; 
loadMyOrders(); 
}

function getCurrentUser(){ 
return JSON.parse(localStorage.getItem('currentUser')||'null'); 
}

function updateAccountUI(){
const u = getCurrentUser();
if(u){
accProfile.style.display='block';
loginForm.style.display='none';
signupForm.style.display='none';
fisherForm.style.display='none';
forgotPasswordForm.style.display='none';
accTitle.innerText = 'Account';
pName.innerText = u.name;
pEmail.innerText = u.email;
pNumber.innerText = u.number;
myAccountBtn.innerText = 'Account ✓';
} else {
accProfile.style.display='none';
loginForm.style.display='block';
signupForm.style.display='none';
fisherForm.style.display='none';
forgotPasswordForm.style.display='none';
accTitle.innerText = 'Login';
myAccountBtn.innerText = 'My Account';
}
}

function prefillUserFields(){
const u = getCurrentUser();
if(u){
uName.value = u.name || '';
uNumber.value = u.number || '';
}
}

// Forget Password functionality
async function sendPasswordReset() {
const email = forgotEmail.value.trim().toLowerCase();
if (!email) {
alert('Please enter your email address');
return;
}

try {
// Check if user exists
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (userSnapshot.empty) {
alert('No account found with this email address');
return;
}

// Generate a 6-digit reset code
const resetCode = Math.floor(100000 + Math.random() * 900000).toString();
const expiryTime = new Date(Date.now() + 3600000).toISOString(); // Code expires in 1 hour

// Store the reset code in Firestore
await db.collection('passwordResets').add({
email,
resetCode,
expiryTime,
used: false
});

// Show the reset code section
document.getElementById('resetCodeSection').style.display = 'block';
alert(`A verification code has been sent to your email. For demo purposes, your code is: ${resetCode}`);
} catch (error) {
console.error("Error sending password reset:", error);
alert("Error sending password reset. Please try again.");
}
}

async function resetPassword() {
const email = forgotEmail.value.trim().toLowerCase();
const code = resetCode.value.trim();
const newPassword = newPassword.value;

if (!email || !code || !newPassword) {
alert('Please fill all fields');
return;
}

try {
// Find the reset code in Firestore
const resetSnapshot = await db.collection('passwordResets')
.where('email', '==', email)
.where('resetCode', '==', code)
.where('used', '==', false)
.get();

if (resetSnapshot.empty) {
alert('Invalid or expired verification code');
return;
}

const resetDoc = resetSnapshot.docs[0];
const resetData = resetDoc.data();

// Check if the code has expired
if (new Date() > new Date(resetData.expiryTime)) {
alert('Verification code has expired');
return;
}

// Mark the reset code as used
await db.collection('passwordResets').doc(resetDoc.id).update({ used: true });

// Find the user and update their password
const userSnapshot = await db.collection('users').where('email', '==', email).get();
if (!userSnapshot.empty) {
const userDoc = userSnapshot.docs[0];
await db.collection('users').doc(userDoc.id).update({ password: newPassword });
}

// Clear the form
forgotEmail.value = '';
resetCode.value = '';
newPassword.value = '';
document.getElementById('resetCodeSection').style.display = 'none';

alert('Password reset successful! You can now login with your new password.');
showLogin();
} catch (error) {
console.error("Error resetting password:", error);
alert("Error resetting password. Please try again.");
}
}

// RATES
async function loadRates(){
try {
const ratesDoc = await db.collection('settings').doc('rates').get();
if (ratesDoc.exists) {
rates = ratesDoc.data();
ratePayeer.value = rates.Payeer;
rateBinance.value = rates.Binance;
} else {
// If rates don't exist in Firestore, use default values
ratePayeer.value = rates.Payeer;
rateBinance.value = rates.Binance;
}
} catch (error) {
console.error("Error loading rates:", error);
// Fallback to default values
ratePayeer.value = rates.Payeer;
rateBinance.value = rates.Binance;
}
}

async function saveRates(){ 
try {
await db.collection('settings').doc('rates').set({
Payeer: Number(ratePayeer.value),
Binance: Number(rateBinance.value)
});

rates.Payeer = Number(ratePayeer.value);
rates.Binance = Number(rateBinance.value);

alert("✔ Dollar Rates Updated");
} catch (error) {
console.error("Error saving rates:", error);
alert("Error updating rates. Please try again.");
}
}

// CALC
function calc(){
const dollar = Number(uDollar.value) || 0;
const cur = uCurrency.value;
const rate = cur === "Payeer" ? rates.Payeer : rates.Binance;
uTaka.value = dollar ? (dollar * rate).toFixed(2) : "";
}

// PLACE ORDER (tempOrder will hold via & tx if user filled)
function placeOrder(){
const current = getCurrentUser();
if(!current){
alert('অর্ডার দিতে হলে প্রথমে Login/Sign Up করুন');
openAccountModal();
return;
}

const name = (uName.value.trim() || current.name);
const number = (uNumber.value.trim() || current.number);
const currency = uCurrency.value;
const dollar = uDollar.value;
const taka = uTaka.value;
const payment = uPayment.value;
const via = uVia.value || "";
const tx = uTx.value.trim() || "";

if(!name || !number || !dollar){
alert('সব ঘর পূরণ করুন');
return;
}

window.tempOrder = { name, number, currency, dollar, taka, payment, via, tx };

cBody.innerHTML = `
<div>নাম: <b>${name}</b></div>
<div>নম্বার: <b>${number}</b></div>
<div>কারেন্সি: <b>${currency}</b></div>
<div>ডলার: <b>${dollar}</b> → টাকা: <b>${taka}</b></div>

<div style="margin-top:10px">পেমেন্ট পাঠানোর আইডি:</div>

<div class="id-badge">
Payeer ID: ${PAYEER_ID}
<button style="float:right;padding:4px 10px" onclick="copyText('${PAYEER_ID}')">Copy</button>
</div>

<div style="height:6px"></div>

<div class="id-badge">
Binance ID: ${BINANCE_ID}
<button style="float:right;padding:4px 10px" onclick="copyText('${BINANCE_ID}')">Copy</button>
</div>
`;

cTx.value = tx;
confirmModal.style.display = "block";
}

async function confirmOrder(){
const tx = cTx.value.trim();
const o = tempOrder;
if(!o) return;

try {
// build new order with trx (tx) and via included
const newOrder = {
name: o.name,
number: o.number,
currency: o.currency,
dollar: o.dollar,
taka: o.taka,
paymentMethod: o.payment,
via: o.via || "",
trx: tx || "",
status: 'PENDING',
createdAt: new Date().toISOString(),
userEmail: getCurrentUser() ? getCurrentUser().email : null,
userType: getCurrentUser() ? getCurrentUser().userType || 'regular' : 'regular'
};

// Add to Firestore
const docRef = await db.collection('orders').add(newOrder);

// Add the ID to the order object for reference
newOrder.id = docRef.id;

confirmModal.style.display="none";
tempOrder=null;

loadMyOrders();
alert("অর্ডার Confirm হয়েছে ✔");

uDollar.value="";
uTaka.value="";
uTx.value="";
uVia.value="";
} catch (error) {
console.error("Error creating order:", error);
alert("Error creating order. Please try again.");
}
}

// LOAD MY ORDERS
function getBanglaStatus(status){
if(status === "COMPLETED") return { text: "✔ অনুমোদিত", cls: "completed" };
if(status === "REJECTED") return { text: "✘ বাতিল করা হয়েছে", cls: "rejected" };
return { text: "⌛ অপেক্ষমাণ", cls: "pending" };
}

async function loadMyOrders(){
try {
const current = getCurrentUser();
myOrders.innerHTML = "";

let ordersQuery;
if(current){
// Check by email OR number
ordersQuery = db.collection('orders').where('userEmail', '==', current.email);
const emailSnapshot = await ordersQuery.get();

const numberQuery = db.collection('orders').where('number', '==', current.number);
const numberSnapshot = await numberQuery.get();

// Combine results and remove duplicates
const emailOrders = emailSnapshot.docs.map(doc => ({id: doc.id, ...doc.data()}));
const numberOrders = numberSnapshot.docs.map(doc => ({id: doc.id, ...doc.data()}));

// Merge arrays, removing duplicates by ID
const allOrders = [...emailOrders];
numberOrders.forEach(order => {
if (!allOrders.find(o => o.id === order.id)) {
allOrders.push(order);
}
});

// Sort by creation date (newest first)
allOrders.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

renderOrders(allOrders);
} else {
const number = uNumber.value.trim();
if(number) {
const numberQuery = db.collection('orders').where('number', '==', number);
const numberSnapshot = await numberQuery.get();
const orders = numberSnapshot.docs.map(doc => ({id: doc.id, ...doc.data()}));

// Sort by creation date (newest first)
orders.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

renderOrders(orders);
} else {
myOrders.innerHTML='<div class="order-empty">আপনার অর্ডার নেই</div>';
}
}
} catch (error) {
console.error("Error loading orders:", error);
myOrders.innerHTML='<div class="order-empty">Error loading orders</div>';
}
}

function renderOrders(orders) {
if(orders.length===0){
myOrders.innerHTML='<div class="order-empty">আপনার অর্ডার নেই</div>';
return;
}

orders.forEach(o=>{
const s = getBanglaStatus(o.status);
const box=document.createElement('div');
box.className='order-box';
box.innerHTML=`
<div class="order-info">
<div><b>${o.name}</b> <span class="small">• ${new Date(o.createdAt).toLocaleString()}</span></div>
<div class="small">${o.currency} • ${o.dollar} USD → ${o.taka} TK • পেমেন্ট: ${o.paymentMethod}</div>
<div class="small">মাধ্যম: ${o.via || 'Not given'}</div>
<div class="small">TXID: ${o.trx || 'Not given'}</div>
</div>

<div class="order-meta">
<div><span class="status ${s.cls}">${s.text}</span></div>
<button onclick="openModal('${o.id}')">View</button>
</div>
`;
myOrders.appendChild(box);
});
}

// ADMIN: Load orders for admin view
async function loadAdmin(){
try {
const q = adminSearch.value.trim();
let ordersQuery = db.collection('orders');

if(q) {
ordersQuery = ordersQuery.where('number', '==', q);
}

const snapshot = await ordersQuery.get();
const orders = snapshot.docs.map(doc => ({id: doc.id, ...doc.data()}));

// Sort by creation date (newest first)
orders.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

adminOrders.innerHTML="";

if(orders.length===0){
adminOrders.innerHTML='<div class="order-empty">কোন অর্ডার পাওয়া যায়নি</div>';
return;
}

orders.forEach(o=>{
const div=document.createElement('div');
div.className='order-box';

div.innerHTML=`
<div style="flex:1">
<b>${o.name}</b> <span class="small">• ${new Date(o.createdAt).toLocaleString()}</span>
<div class="small">নম্বর: ${o.number} • ${o.currency} • ${o.dollar} USD → ${o.taka} TK</div>
<div class="small">মাধ্যম: ${o.via || 'Not given'}</div>
<div>TXID: <span class="small">${o.trx||'—'}</span></div>
</div>

<div style="min-width:150px;text-align:right">
<div><span class="status ${o.status==='Pending'?'pending':o.status==='COMPLETED'?'completed':'rejected'}">${o.status}</span></div>

<button onclick="adminChangeStatus('${o.id}','COMPLETED')">Approve</button>
<button onclick="adminChangeStatus('${o.id}','REJECTED')">Reject</button>
<button onclick="adminChangeStatus('${o.id}','PENDING')">Pending</button>
</div>
`;

adminOrders.appendChild(div);
});
} catch (error) {
console.error("Error loading admin orders:", error);
adminOrders.innerHTML='<div class="order-empty">Error loading orders</div>';
}
}

// ADMIN: change status (require trx when approving)
async function adminChangeStatus(id,newStatus){
try {
if(newStatus==='COMPLETED') {
const orderDoc = await db.collection('orders').doc(id).get();
if (!orderDoc.exists) {
alert("Order not found");
return;
}

const orderData = orderDoc.data();
if(!orderData.trx || orderData.trx.trim()==''){
alert("⚠ TXID ছাড়া Approve করা যাবে না!");
return;
}
}

await db.collection('orders').doc(id).update({
status: newStatus
});

loadAdmin();
loadMyOrders();
alert("Status Updated");
} catch (error) {
console.error("Error updating status:", error);
alert("Error updating status. Please try again.");
}
}

// MODAL for specific order
let currentModalId=null;
async function openModal(id){
currentModalId=id;

try {
const orderDoc = await db.collection('orders').doc(id).get();
if (!orderDoc.exists) return;

const o = {id: orderDoc.id, ...orderDoc.data()};

mTitle.innerText="Order — "+o.name;

mBody.innerHTML=`
<div class="small">Created: ${new Date(o.createdAt).toLocaleString()}</div>
<div>নাম: <b>${o.name}</b></div>
<div>নম্বর: <b>${o.number}</b></div>
<div>কারেন্সি: <b>${o.currency}</b></div>
<div>ডলার: <b>${o.dollar}</b> → টাকা: <b>${o.taka}</b></div>

<div style="margin-top:8px">বর্তমান স্ট্যাটাস: <b>${o.status}</b></div>
`;

mTx.value = o.trx || "";
modal.style.display="block";
} catch (error) {
console.error("Error opening order:", error);
alert("Error loading order details");
}
}

function closeModal(event){
// Check if the click was on the modal background or the close button
if (!event || event.target === modal || event.target.textContent === 'Close') {
modal.style.display='none'; 
currentModalId=null;
}
}

function closeConfirm(event){
// Check if the click was on the modal background or the close button
if (!event || event.target === confirmModal || event.target.textContent === 'Close') {
confirmModal.style.display='none';
}
}

async function saveTx(){
if(!currentModalId) return;

const tx = mTx.value.trim();

try {
await db.collection('orders').doc(currentModalId).update({
trx: tx
});

loadAdmin();
loadMyOrders();
alert("Transaction ID Updated");

closeModal();
} catch (error) {
console.error("Error updating transaction ID:", error);
alert("Error updating transaction ID. Please try again.");
}
}

// COPY
function copyText(text){ 
navigator.clipboard.writeText(text).then(() => {
alert("Copied: " + text);
}).catch(err => {
console.error('Could not copy text: ', err);
alert("Failed to copy text");
});
}

// ONLINE/OFFLINE
function updateStatus(){
const hour = new Date().getHours();
if(hour>=22 || hour<9){
opStatus.innerText='Offline';
opStatus.className='status-badge offline';
} else {
opStatus.innerText='Online';
opStatus.className='status-badge online';
}
}
setInterval(updateStatus,60000);
updateStatus();

// VIEW SWITCH
function showUser(){ userArea.style.display='block'; adminArea.style.display='none'; }

// ADMIN LOGIN CHECK
function checkAdmin(){
const pass = adminPass.value.trim();
if(pass === "saimon500"){ 
adminLogin.style.display="none"; 
showAdmin(); 
} else { 
alert("❌ Wrong Password!"); 
}
}

function showAdmin(){ 
userArea.style.display='none'; 
adminArea.style.display='block'; 
loadAdmin(); 
loadRates(); 
}

// ON LOAD
window.addEventListener('load',()=>{
loadMyOrders();
loadAdmin();
loadRates();
updateAccountUI();
prefillUserFields();
});
</script>

</body>
</html>
