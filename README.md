<!DOCTYPE html>
<html lang="ro">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Magazin Handmade & Prefabricate</title>
<style>
body{font-family:Arial,Helvetica,sans-serif;margin:0;background:#fafafa}
header{background:#6b4f4f;color:white;padding:20px;text-align:center}
nav{background:#e6d5d5;padding:10px;text-align:center}
nav a{margin:0 15px;text-decoration:none;color:#333;font-weight:bold}
.container{padding:20px;max-width:1100px;margin:auto}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:20px}
.card{background:white;border-radius:12px;box-shadow:0 2px 6px rgba(0,0,0,.15);padding:15px;text-align:center}
.card img{width:100%;height:200px;object-fit:cover;border-radius:8px}
button{background:#6b4f4f;color:white;border:none;padding:10px 15px;border-radius:8px;cursor:pointer}
button:hover{background:#4a3434}
#cart{position:fixed;right:20px;bottom:20px;background:white;padding:15px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,.2);width:260px}
footer{background:#6b4f4f;color:white;text-align:center;padding:15px;margin-top:40px}
</style>
</head>
<body>
<header>
<h1>Magazin Handmade & Produse Prefabricate</h1>
<p>Pachete cadou | Produse lucrate manual | Produse gata fabricate</p>
</header>
<nav>
<a href="#produse">Produse</a>
<a href="#contact">Contact</a>
</nav>

<div class="container" id="produse">
<h2>Produsele Noastre</h2>
<div class="products" id="product-list"></div>
</div>

<div id="cart">
<h3>Coș</h3>
<ul id="cart-items"></ul>
<strong>Total: <span id="total">0</span> lei</strong>
</div>

<div class="container" id="contact">
<h2>Contact</h2>
<p>Email: contact@magazinulmeu.ro</p>
<p>Telefon: 07xx xxx xxx</p>
</div>

<footer>
© 2026 Magazinul Meu
</footer>

<script>
const products=[
{id:1,name:"Pachet cadou handmade",price:120,img:"https://picsum.photos/400?1"},
{id:2,name:"Lumânare artizanală",price:35,img:"https://picsum.photos/400?2"},
{id:3,name:"Set decorativ prefabricat",price:90,img:"https://picsum.photos/400?3"},
{id:4,name:"Tablou handmade",price:150,img:"https://picsum.photos/400?4"}
];

let cart=[];
const list=document.getElementById("product-list");
const cartItems=document.getElementById("cart-items");
const total=document.getElementById("total");

products.forEach(p=>{
const el=document.createElement("div");
el.className="card";
el.innerHTML=`<img src="${p.img}"><h3>${p.name}</h3><p>${p.price} lei</p><button onclick="addToCart(${p.id})">Adaugă</button>`;
list.appendChild(el);
});

function addToCart(id){
const product=products.find(p=>p.id===id);
cart.push(product);
renderCart();
}

function renderCart(){
cartItems.innerHTML="";
let sum=0;
cart.forEach(item=>{
sum+=item.price;
const li=document.createElement("li");
li.textContent=item.name+" - "+item.price+" lei";
cartItems.appendChild(li);
});
total.textContent=sum;
}
</script>
</body>
</html>
