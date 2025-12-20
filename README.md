  CREATE DATABASE wallet_app;
USE wallet_app;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50),
  password VARCHAR(255),
  balance DECIMAL(10,2) DEFAULT 0
);

CREATE TABLE transactions (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT,
  amount DECIMAL(10,2),
  type ENUM('deposit','withdraw'),
  status ENUM('pending','approved'),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);const express = require('express');
const mysql = require('mysql');
const bcrypt = require('bcrypt');
const app = express();

app.use(express.json());
app.use(express.static('public'));

const db = mysql.createConnection({
  host:'localhost',
  user:'root',
  password:'',
  database:'wallet_app'
});

db.connect();

// Register
app.post('/register', async (req,res)=>{
  const {username,password} = req.body;
  const hash = await bcrypt.hash(password,10);
  db.query(
    "INSERT INTO users(username,password) VALUES (?,?)",
    [username,hash],
    ()=>res.send("Registered")
  );
});

// Login
app.post('/login',(req,res)=>{
  const {username,password} = req.body;
  db.query(
    "SELECT * FROM users WHERE username=?",
    [username],
    async (err,result)=>{
      if(result.length && await bcrypt.compare(password,result[0].password)){
        res.json(result[0]);
      } else res.status(401).send("Invalid");
    }
  );
});

// Deposit (Demo)
app.post('/deposit',(req,res)=>{
  const {user_id,amount} = req.body;
  db.query(
    "INSERT INTO transactions(user_id,amount,type,status) VALUES (?,?, 'deposit','approved')",
    [user_id,amount]
  );
  db.query(
    "UPDATE users SET balance = balance + ? WHERE id=?",
    [amount,user_id]
  );
  res.send("Deposit Success");
});

// Withdraw
app.post('/withdraw',(req,res)=>{
  const {user_id,amount} = req.body;
  db.query(
    "INSERT INTO transactions(user_id,amount,type,status) VALUES (?,?, 'withdraw','pending')",
    [user_id,amount]
  );
  res.send("Withdraw Requested");
});

app.listen(3000,()=>console.log("Server running"));<input id="u" placeholder="Username">
<input id="p" type="password" placeholder="Password">
<button onclick="reg()">Register</button>

<script>
function reg(){
 fetch('/register',{
  method:'POST',
  headers:{'Content-Type':'application/json'},
  body:JSON.stringify({username:u.value,password:p.value})
 });
}
</script><input id="u">
<input id="p" type="password">
<button onclick="login()">Login</button>

<script>
function login(){
 fetch('/login',{
  method:'POST',
  headers:{'Content-Type':'application/json'},
  body:JSON.stringify({username:u.value,password:p.value})
 })
 .then(r=>r.json())
 .then(d=>{
   localStorage.setItem("user",JSON.stringify(d));
   location='dashboard.html';
 });
}
                       </script><h2 id="bal"></h2>

<input id="amt" placeholder="Amount">
<button onclick="dep()">Deposit</button>
<button onclick="wd()">Withdraw</button>

<script>
let u = JSON.parse(localStorage.getItem("user"));
bal.innerText = "Balance: "+u.balance;

function dep(){
 fetch('/deposit',{
  method:'POST',
  headers:{'Content-Type':'application/json'},
  body:JSON.stringify({user_id:u.id,amount:amt.value})
 }).then(()=>alert("Deposited"));
}

function wd(){
 fetch('/withdraw',{
  method:'POST',
  headers:{'Content-Type':'application/json'},
  body:JSON.stringify({user_id:u.id,amount:amt.value})
 }).then(()=>alert("Withdraw Requested"));
}
       </script>
