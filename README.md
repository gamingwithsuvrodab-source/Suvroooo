<!DOCTYPE html>
<html>
<head>
<title>Facebook Style Site</title>
<style>
body{margin:0;font-family:Arial;background:#f0f2f5}
.nav{background:#1877f2;color:white;padding:10px;font-size:22px}
.container{width:500px;margin:auto;margin-top:20px}
.card{background:white;padding:15px;border-radius:6px;margin-bottom:10px}
input,textarea{width:100%;padding:8px;margin:5px 0}
button{background:#1877f2;color:white;border:none;padding:8px;width:100%;cursor:pointer}
.post{border-top:1px solid #ddd;padding-top:10px;margin-top:10px}
small{color:gray}
.like{color:blue;cursor:pointer}
.hide{display:none}
</style>
</head>

<body>

<div class="nav">facebook</div>

<div class="container">

<!-- LOGIN -->
<div id="login" class="card">
<h3>Login</h3>
<input id="lemail" placeholder="Email">
<input id="lpass" type="password" placeholder="Password">
<button onclick="login()">Login</button>
<p onclick="showRegister()" style="cursor:pointer;color:blue">Create Account</p>
</div>

<!-- REGISTER -->
<div id="register" class="card hide">
<h3>Register</h3>
<input id="rname" placeholder="Name">
<input id="remail" placeholder="Email">
<input id="rpass" type="password" placeholder="Password">
<button onclick="register()">Register</button>
</div>

<!-- HOME -->
<div id="home" class="hide">

<div class="card">
<b id="username"></b>
<button onclick="logout()">Logout</button>
</div>

<div class="card">
<textarea id="postText" placeholder="What's on your mind?"></textarea>
<button onclick="addPost()">Post</button>
</div>

<div id="feed"></div>

</div>
</div>

<script>
let users = JSON.parse(localStorage.getItem("users")) || [];
let posts = JSON.parse(localStorage.getItem("posts")) || [];
let currentUser = JSON.parse(localStorage.getItem("currentUser"));

if(currentUser) showHome();

function showRegister(){
 login.classList.add("hide");
 register.classList.remove("hide");
}

function register(){
 let u={name:rname.value,email:remail.value,pass:rpass.value};
 users.push(u);
 localStorage.setItem("users",JSON.stringify(users));
 alert("Registered");
 location.reload();
}

function login(){
 let u=users.find(x=>x.email==lemail.value && x.pass==lpass.value);
 if(u){
  localStorage.setItem("currentUser",JSON.stringify(u));
  showHome();
 }else alert("Wrong Login");
}

function showHome(){
 login.classList.add("hide");
 register.classList.add("hide");
 home.classList.remove("hide");
 username.innerText=currentUser.name;
 loadPosts();
}

function logout(){
 localStorage.removeItem("currentUser");
 location.reload();
}

function addPost(){
 let p={user:currentUser.name,text:postText.value,likes:0,comments:[]};
 posts.unshift(p);
 localStorage.setItem("posts",JSON.stringify(posts));
 postText.value="";
 loadPosts();
}

function loadPosts(){
 feed.innerHTML="";
 posts.forEach((p,i)=>{
  feed.innerHTML+=`
  <div class="card post">
   <b>${p.user}</b>
   <p>${p.text}</p>
   <span class="like" onclick="like(${i})">Like (${p.likes})</span>
   <div>
    <input placeholder="Comment" onkeydown="if(event.key=='Enter')comment(${i},this)">
    ${p.comments.map(c=>"<small>"+c+"</small><br>").join("")}
   </div>
  </div>`;
 });
}

function like(i){
 posts[i].likes++;
 localStorage.setItem("posts",JSON.stringify(posts));
 loadPosts();
}

function comment(i,el){
 posts[i].comments.push(el.value);
 el.value="";
 localStorage.setItem("posts",JSON.stringify(posts));
 loadPosts();
}
</script>

</body>
</html>
