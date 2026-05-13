# 2FA
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Two Factor Authentication Demo</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:'Poppins',sans-serif;
}
body{
height:100vh;
display:flex;
justify-content:center;
align-items:center;
background:linear-gradient(135deg,#4facfe,#00f2fe);
}
.container{
background:white;
padding:40px;
width:350px;
border-radius:12px;
box-shadow:0 10px 25px rgba(0,0,0,0.2);
text-align:center;
}
h2{
margin-bottom:20px;
color:#333;
}
input{
width:100%;
padding:10px;
margin:10px 0;
border:1px solid #ccc;
border-radius:6px;
font-size:14px;
}
button{
width:100%;
padding:10px;
background:#4facfe;
border:none;
color:white;
font-size:16px;
border-radius:6px;
cursor:pointer;
transition:0.3s;
}
button:hover{
background:#0077ff;
}
#otpSection{
display:none;
margin-top:10px;
}
#otpDisplay{
margin-top:10px;
font-weight:600;
color:#0077ff;
}
.success{
color:green;
font-weight:600;
margin-top:10px;
}
.error{
color:red;
margin-top:10px;
}
</style>

<script>
let generatedOTP = 0;
const correctPassword = "1234";

function login(){
let password = document.getElementById("password").value.trim();
let message = document.getElementById("message");

if(password === correctPassword){
generatedOTP = Math.floor(1000 + Math.random() * 9000);

document.getElementById("otpSection").style.display = "block";
document.getElementById("otpDisplay").innerText = "Demo OTP: " + generatedOTP;

message.innerText = "Password Correct. Enter OTP.";
message.className = "";
}else{
message.innerText = "Wrong Password!";
message.className = "error";
document.getElementById("otpSection").style.display = "none";
}
}

function verifyOTP(){
let userOTP = document.getElementById("otp").value.trim();
let message = document.getElementById("message");

if(userOTP === generatedOTP.toString()){
message.innerText = "Login Successful ✔";
message.className = "success";
}else{
message.innerText = "Invalid OTP!";
message.className = "error";
}
}
</script>

</head>

<body>
<div class="container">
<h2>Two-Factor Authentication</h2>

<input type="text" placeholder="Username">
<input type="password" id="password" placeholder="Password">

<button type="button" onclick="login()">Login</button>

<div id="otpSection">
<p id="otpDisplay"></p>
<input type="text" id="otp" placeholder="Enter OTP">
<button type="button" onclick="verifyOTP()">Verify OTP</button>
</div>

<p id="message"></p>

</div>
</body>
</html>
