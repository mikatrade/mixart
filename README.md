<!DOCTYPE html>
<html lang="ro">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>MixArt – Magazin Online</title>

<style>
  body{font-family:Arial,Helvetica,sans-serif;margin:0;background:#fafafa}
  header{background:#6b4f4f;color:white}
  .topbar{display:flex;align-items:center;justify-content:space-between;padding:12px 18px;gap:12px}
  .brand{display:flex;align-items:center;gap:12px}
  .brand img{height:48px}
  nav{background:#e6d5d5;padding:10px;text-align:center}
  nav a{margin:0 15px;text-decoration:none;color:#333;font-weight:bold}
  .container{padding:20px;max-width:1100px;margin:auto}
  .hero img{width:100%;border-radius:14px;box-shadow:0 6px 18px rgba(0,0,0,.12)}
  .category-bar{text-align:center;margin-top:15px}
  button{background:#6b4f4f;color:white;border:none;padding:10px 15px;border-radius:10px;margin:6px;cursor:pointer}
  button:hover{background:#4a3434}
  .products{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:20px}
  .card{background:white;border-radius:12px;box-shadow:0 2px 6px rgba(0,0,0,.15);padding:15px;text-align:center}
  .card img{width:100%;height:200px;object-fit:cover;border-radius:8px}
  #cart{position:fixed;right:20px;bottom:20px;background:white;padding:15px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,.2);width:260px}
  footer{background:#6b4f4f;color:white;text-align:center;padding:15px;margin-top:40px}
</style>
</head>

<body>

<header>
  <div class="topbar">
    <div class="brand">
      <img src="images/logo-mixart.png">
      <div>
        <strong>MixArt</strong><br>
        <small>Magazin online</small>
      </div>
    </div>

    <!-- CONTACT HEADER -->
    <div style="text-align:right;font-size:14px">
      📞 0762 100 997<br>
      ✉ office.mikatrade@yahoo.com
    </div>
  </div>
</header>

<nav>
  <a href="#produse">Produse</a>
  <a href="#contact">Contact</a>
</nav>

<div class="container hero">
  <img src="images/hero.png">
</div>

<div class="category-bar">
  <button onclick="showCategory('toate')">Toate</button>
  <button onclick="showCategory('sezoniere')">Produse sezoniere</button>
  <button onclick="showCategory('jucarii')">Jucării</button>
  <button onclick="showCategory('decoratiuni')">Decorațiuni</button>
  <button onclick="showCategory('papetarie')">Papetărie</button>
  <button onclick="showCategory('petreceri')">Petreceri</button>
  <button onclick="showCategory('petshop')">Pet Shop</button>
  <button onclick="showCategory('cadouri')">Cadouri</button>
</div>

<div class="container" id="produse">
  <h2>Produsele Noastre</h2>
  <div class="products" id="product-list"></div>
</div>

<div id="cart">
  <h3>Coș</h3>
  <ul id="cart-items"></ul>
  <strong>Total: <span id="total">0</span> lei</strong>
</div>

<!-- CONTACT SECTION -->
<div class="container" id="contact">
  <h2>Contact</h2>
  <p><strong>Telefon:</strong> 0762 100 997</p>
  <p><strong>Email:</strong> office.mikatrade@yahoo.com</p>
</div>

<footer>© 2026 MixArt</footer>

<script>
const products=[
{id:1,name:"Mărțișor pisicuță glitter",price:8,category:"sezoniere",img:"images/martisor-pisica.webp"},
{id:2,name:"Set mărțișoare",price:25,category:"sezoniere",img:"https://picsum.photos/400?1"},
{id:3,name:"Jucărie pluș",price:45,category:"jucarii",img:"https://picsum.photos/400?2"},
{id:4,name:"Tablou handmade",price:150,category:"decoratiuni",img:"https://picsum.photos/400?3"},
{id:5,name:"Caiet personalizat",price:30,category:"papetarie",img:"https://picsum.photos/400?4"},
{id:6,name:"Set petrecere",price:22,category:"petreceri",img:"https://picsum.photos/400?5"},
{id:7,name:"Jucărie pisici",price:15,category:"petshop",img:"https://picsum.photos/400?6"},
{id:8,name:"Pachet cadou",price:120,category:"cadouri",img:"https://picsum.photos/400?7"}
];

let cart=[];
const list=document.getElementById("product-list");
const cartItems=document.getElementById("cart-items");
const total=document.getElementById("total");

function renderProducts(filter="toate"){
  list.innerHTML="";
  const filtered=(filter==="toate")?products:products.filter(p=>p.category===filter);
  filtered.forEach(p=>{
    const el=document.createElement("div");
    el.className="card";
    el.innerHTML=`<img src="${p.img}"><h3>${p.name}</h3><p>${p.price} lei</p><button onclick="addToCart(${p.id})">Adaugă</button>`;
    list.appendChild(el);
  });
}

function showCategory(cat){renderProducts(cat);}
function addToCart(id){cart.push(products.find(p=>p.id===id));renderCart();}
function renderCart(){
  cartItems.innerHTML="";let sum=0;
  cart.forEach(i=>{sum+=i.price;const li=document.createElement("li");li.textContent=i.name+" - "+i.price+" lei";cartItems.appendChild(li);});
  total.textContent=sum;
}
renderProducts();
</script>

</body>
</html>
