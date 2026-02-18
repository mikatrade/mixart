<!DOCTYPE html>
<html lang="ro">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>MixArt – Magazin Online</title>
<style>
body{font-family:Arial,Helvetica,sans-serif;margin:0;background:#fafafa}
header{background:#6b4f4f;color:white;padding:20px;text-align:center}
nav{background:#e6d5d5;padding:10px;text-align:center}
nav a{margin:0 15px;text-decoration:none;color:#333;font-weight:bold}
.container{padding:20px;max-width:1100px;margin:auto}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:20px}
.card{background:white;border-radius:12px;box-shadow:0 2px 6px rgba(0,0,0,.15);padding:15px;text-align:center}
.card img{width:100%;height:200px;object-fit:cover;border-radius:8px}
button{background:#6b4f4f;color:white;border:none;padding:10px 15px;border-radius:8px;cursor:pointer;margin:6px}
button:hover{background:#4a3434}
#cart{position:fixed;right:20px;bottom:20px;background:white;padding:15px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,.2);width:260px}
footer{background:#6b4f4f;color:white;text-align:center;padding:15px;margin-top:40px}
.small-note{font-size:12px;opacity:.85;margin-top:6px}
</style>
</head>
<body>
<header>
  <h1>MixArt – Magazin Online</h1>
  <p>Produse sezoniere | Jucării | Decorațiuni | Papetărie | Petreceri | Pet Shop | Pachete Handmade/Cadouri</p>
</header>
<nav>
  <a href="#produse">Produse</a>
  <a href="#contact">Contact</a>
</nav>

<div class="container" id="produse">
  <h2>Produsele Noastre</h2>

  <!-- BUTOANE CATEGORII -->
  <div style="text-align:center;margin-bottom:14px">
    <button onclick="showCategory('toate')">Toate</button>
    <button onclick="showCategory('sezoniere')">Produse sezoniere</button>
    <button onclick="showCategory('jucarii')">Jucării</button>
    <button onclick="showCategory('decoratiuni')">Decorațiuni</button>
    <button onclick="showCategory('papetarie')">Papetărie</button>
    <button onclick="showCategory('petreceri')">Produse pentru petreceri</button>
    <button onclick="showCategory('petshop')">Produse Pet Shop</button>
    <button onclick="showCategory('cadouri')">Pachete Handmade/Cadouri</button>
    <div class="small-note">Apasă pe o categorie ca să filtrezi produsele.</div>
  </div>

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
  © 2026 MixArt
</footer>

<script>
/*
  CATEGORII:
  - sezoniere
  - jucarii
  - decoratiuni
  - papetarie
  - petreceri
  - petshop
  - cadouri
*/

const products=[
// PRODUSE SEZONIERE
{id:1, name:"Mărțișor pisicuță glitter", price:8, category:"sezoniere", img:"images/martisor-pisica.webp"},
{id:2, name:"Set 5 mărțișoare (model mixt)", price:25, category:"sezoniere", img:"https://picsum.photos/400?sez1"},

// JUCARII
{id:3, name:"Jucărie pluș (model)", price:45, category:"jucarii", img:"https://picsum.photos/400?juc1"},
{id:4, name:"Jucărie educativă (model)", price:55, category:"jucarii", img:"https://picsum.photos/400?juc2"},

// DECORATIUNI
{id:5, name:"Tablou decorativ handmade", price:150, category:"decoratiuni", img:"https://picsum.photos/400?dec1"},
{id:6, name:"Lumânare decorativă", price:35, category:"decoratiuni", img:"https://picsum.photos/400?dec2"},

// PAPETARIE
{id:7, name:"Caiet/Agendă (model)", price:30, category:"papetarie", img:"https://picsum.photos/400?pap1"},
{id:8, name:"Set felicitări (model)", price:20, category:"papetarie", img:"https://picsum.photos/400?pap2"},

// PRODUSE PENTRU PETRECERI
{id:9, name:"Baloane folie (model)", price:18, category:"petreceri", img:"https://picsum.photos/400?pet1"},
{id:10, name:"Set farfurii/pahare (model)", price:22, category:"petreceri", img:"https://picsum.photos/400?pet2"},

// PRODUSE PET SHOP
{id:11, name:"Jucărie pentru pisici (model)", price:15, category:"petshop", img:"https://picsum.photos/400?ps1"},
{id:12, name:"Bol hrană animale (model)", price:28, category:"petshop", img:"https://picsum.photos/400?ps2"},

// PACHETE HANDMADE / CADOURI
{id:13, name:"Pachet cadou handmade", price:120, category:"cadouri", img:"https://picsum.photos/400?cad1"},
{id:14, name:"Cutie cadou premium", price:110, category:"cadouri", img:"https://picsum.photos/400?cad2"}
];

let cart=[];
const list=document.getElementById("product-list");
const cartItems=document.getElementById("cart-items");
const total=document.getElementById("total");

function renderProducts(filter="toate"){
  list.innerHTML="";

  const filtered = (filter==="toate")
    ? products
    : products.filter(p => p.category === filter);

  filtered.forEach(p=>{
    const el=document.createElement("div");
    el.className="card";
    el.innerHTML=`<img src="${p.img}" alt="${p.name}">
      <h3>${p.name}</h3>
      <p>${p.price} lei</p>
      <button onclick="addToCart(${p.id})">Adaugă</button>`;
    list.appendChild(el);
  });
}

function showCategory(cat){
  renderProducts(cat);
}

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

// afiseaza toate produsele la incarcare
renderProducts();
</script>
</body>
</html>
