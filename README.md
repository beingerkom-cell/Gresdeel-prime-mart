
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="GRESDEEL PRIME MART - Global online shopping">
<title>GRESDEEL PRIME MART</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:Arial,sans-serif;background:#f4f4f4;color:#222}
header{background:#101820;color:white;text-align:center;padding:23px 10px}
.logo{font-size:25px;color:#d6ad60;font-weight:bold}
header p{margin-top:8px;font-size:13px}
nav{background:#202c36;padding:14px;text-align:center}
nav a{color:white;text-decoration:none;margin:0 10px}
.hero{background:linear-gradient(120deg,#101820,#394957);color:white;text-align:center;padding:55px 15px}
.hero h1{color:#d6ad60;font-size:30px;margin-bottom:15px}
.hero p{line-height:1.6;margin-bottom:20px}
button{cursor:pointer}
.gold{background:#d6ad60;border:0;padding:13px 22px;border-radius:5px;font-weight:bold}
.container{max-width:1100px;margin:auto;padding:20px 13px}
h2{margin:15px 0}
.search{width:100%;padding:14px;border:1px solid #ddd;border-radius:7px;font-size:16px;margin:12px 0}
.categories{display:flex;gap:9px;overflow-x:auto;padding:10px 0 20px}
.cat{background:white;border:0;padding:12px 17px;border-radius:22px;white-space:nowrap}
.cat.active{background:#101820;color:white}
.products{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:13px}
.product{background:white;border-radius:9px;padding:12px;box-shadow:0 2px 8px #ddd}
.pic{height:115px;background:#eee;border-radius:7px;display:grid;place-items:center;font-size:53px}
.product h3{font-size:15px;margin:12px 0 7px}
.price{color:#16834a;font-weight:bold;margin-bottom:12px}
.add{width:100%;background:#101820;color:white;border:0;padding:12px;border-radius:5px}
.cart{background:white;margin-top:25px;padding:17px;border-radius:9px}
.cartrow{display:flex;justify-content:space-between;align-items:center;gap:8px;padding:12px 0;border-bottom:1px solid #eee}
.remove{background:#d94343;color:white;border:0;padding:7px;border-radius:4px}
.total{font-size:19px;font-weight:bold;margin:18px 0}
.checkout{background:#16834a;color:white;border:0;padding:15px;width:100%;border-radius:6px;font-weight:bold}
.info{background:white;text-align:center;padding:25px 15px;line-height:1.8;margin-top:20px}
footer{background:#101820;color:white;text-align:center;padding:25px;line-height:1.8;margin-top:25px}
footer strong{color:#d6ad60}
@media(min-width:650px){.products{grid-template-columns:repeat(3,1fr)}.hero h1{font-size:42px}}
@media(min-width:950px){.products{grid-template-columns:repeat(4,1fr)}}
</style>
</head>
<body>
<header>
<div class="logo">GRESDEEL PRIME MART</div>
<p>Your World. Your Shopping. One Destination.</p>
</header>
<nav>
<a href="#home">Home</a>
<a href="#shop">Shop</a>
<a href="#cart">Cart 🛒</a>
<a href="#about">About</a>
</nav>
<section class="hero" id="home">
<h1>SHOP THE WORLD</h1>
<p>Discover amazing products and enjoy a better shopping experience.</p>
<button class="gold" onclick="document.getElementById('shop').scrollIntoView()">START SHOPPING</button>
</section>
<main class="container" id="shop">
<h2>Explore Our Store</h2>
<input class="search" id="search" placeholder="Search products..." type="search">
<div class="categories">
<button class="cat active" onclick="filterCategory('All',this)">All</button>
<button class="cat" onclick="filterCategory('Fashion',this)">Fashion</button>
<button class="cat" onclick="filterCategory('Electronics',this)">Electronics</button>
<button class="cat" onclick="filterCategory('Beauty',this)">Beauty</button>
<button class="cat" onclick="filterCategory('Home',this)">Home</button>
<button class="cat" onclick="filterCategory('Accessories',this)">Accessories</button>
</div>
<div class="products" id="products"></div>
<section class="cart" id="cart">
<h2>🛒 Your Shopping Cart</h2>
<div id="cartItems">Your cart is empty.</div>
<div class="total" id="total">Total: ₦0</div>
<button class="checkout" onclick="checkout()">ORDER THROUGH WHATSAPP</button>
</section>
</main>
<section class="info" id="about">
<h2>About GRESDEEL PRIME MART</h2>
<p>Bringing different shopping categories together in one place.</p>
<p>Starting currency: Nigerian Naira (NGN).</p>
<p>Our goal is to serve customers worldwide.</p>
</section>
<footer>
<strong>GRESDEEL PRIME MART</strong>
<p>Quality Shopping. Global Experience.</p>
<p>© 2026 GRESDEEL PRIME MART</p>
</footer>
<script>
const products=[
{id:1,name:"Classic Sneakers",price:25000,category:"Fashion",emoji:"👟"},
{id:2,name:"Luxury Wrist Watch",price:18000,category:"Accessories",emoji:"⌚"},
{id:3,name:"Wireless Headphones",price:35000,category:"Electronics",emoji:"🎧"},
{id:4,name:"Smartphone",price:180000,category:"Electronics",emoji:"📱"},
{id:5,name:"Premium Perfume",price:22000,category:"Beauty",emoji:"🧴"},
{id:6,name:"Skincare Collection",price:28000,category:"Beauty",emoji:"🧼"},
{id:7,name:"Modern Table Lamp",price:15000,category:"Home",emoji:"💡"},
{id:8,name:"Travel Backpack",price:20000,category:"Fashion",emoji:"🎒"},
{id:9,name:"Sunglasses",price:12000,category:"Accessories",emoji:"🕶️"},
{id:10,name:"Bluetooth Speaker",price:30000,category:"Electronics",emoji:"🔊"},
{id:11,name:"Home Decoration",price:17000,category:"Home",emoji:"🏠"},
{id:12,name:"Fashion Handbag",price:32000,category:"Fashion",emoji:"👜"}
];
const money=new Intl.NumberFormat("en-NG",{style:"currency",currency:"NGN",maximumFractionDigits:0});
let cart=[];
let category="All";
function showProducts(){
const query=document.getElementById("search").value.toLowerCase();
const area=document.getElementById("products");
area.innerHTML="";
const found=products.filter(p=>(category==="All"||p.category===category)&&p.name.toLowerCase().includes(query));
if(!found.length){area.textContent="No products found.";return;}
found.forEach(p=>{
const card=document.createElement("div");
card.className="product";
const pic=document.createElement("div");
pic.className="pic";
pic.textContent=p.emoji;
const name=document.createElement("h3");
name.textContent=p.name;
const price=document.createElement("p");
price.className="price";
price.textContent=money.format(p.price);
const btn=document.createElement("button");
btn.className="add";
btn.textContent="ADD TO CART";
btn.onclick=()=>addToCart(p.id);
card.append(pic,name,price,btn);
area.appendChild(card);
});
}
document.getElementById("search").addEventListener("input",showProducts);
function filterCategory(value,btn){
category=value;
document.querySelectorAll(".cat").forEach(b=>b.classList.remove("active"));
btn.classList.add("active");
showProducts();
}
function addToCart(id){
const item=cart.find(x=>x.id===id);
if(item)item.quantity++;
else cart.push({id,quantity:1});
updateCart();
}
function updateCart(){
const area=document.getElementById("cartItems");
area.innerHTML="";
let total=0;
if(!cart.length)area.textContent="Your cart is empty.";
cart.forEach(item=>{
const p=products.find(x=>x.id===item.id);
if(!p)return;
total+=p.price*item.quantity;
const row=document.createElement("div");
row.className="cartrow";
const name=document.createElement("span");
name.textContent=p.name+" x "+item.quantity;
const price=document.createElement("strong");
price.textContent=money.format(p.price*item.quantity);
const remove=document.createElement("button");
remove.className="remove";
remove.textContent="Remove";
remove.onclick=()=>{cart=cart.filter(x=>x.id!==item.id);updateCart();};
row.append(name,price,remove);
area.appendChild(row);
});
document.getElementById("total").textContent="Total: "+money.format(total);
}
function checkout(){
if(!cart.length){alert("Add a product first!");return;}
const phone="234XXXXXXXXXX";
if(!/^234\d{10}$/.test(phone)){
alert("The store WhatsApp number has not been added yet.");
return;
}
let message="Hello GRESDEEL PRIME MART! I want to order:\n\n";
let total=0;
cart.forEach(item=>{
const p=products.find(x=>x.id===item.id);
message+=p.name+" x "+item.quantity+" - "+money.format(p.price*item.quantity)+"\n";
total+=p.price*item.quantity;
});
message+="\nTotal: "+money.format(total);
window.open("https://wa.me/"+phone+"?text="+encodeURIComponent(message),"_blank");
}
showProducts();
updateCart();
</script>
</body>
</html>
