<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Worex Shop - PUBG & Store</title>

<style>
body{
    margin:0;
    font-family:Arial, sans-serif;
    background:#0f0f0f;
    color:white;
}

header{
    background:#ff3c00;
    padding:20px;
    text-align:center;
    font-size:24px;
    font-weight:bold;
}

nav{
    background:#1a1a1a;
    text-align:center;
    padding:10px;
}

nav button{
    margin:5px;
    padding:10px 15px;
    border:none;
    border-radius:10px;
    background:#ff3c00;
    color:white;
    cursor:pointer;
}

.container{
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
}

.card{
    background:#1c1c1c;
    margin:15px;
    padding:15px;
    width:250px;
    border-radius:15px;
    text-align:center;
}

.card img{
    width:100%;
    border-radius:10px;
}

button{
    margin-top:10px;
    padding:10px;
    width:100%;
    border:none;
    border-radius:10px;
    background:#ff3c00;
    color:white;
    font-weight:bold;
    cursor:pointer;
}

footer{
    text-align:center;
    padding:15px;
    margin-top:20px;
    background:#111;
}
</style>
</head>

<body>

<header>WOREX SHOP</header>

<nav>
<button onclick="showSection('pubg')">PUBG UC</button>
<button onclick="showSection('store')">Mağaza</button>
<button onclick="showCart()">Sepet (<span id="cartCount">0</span>)</button>
</nav>

<div id="content"></div>

<footer>
© 2026 Worex Shop - Tüm Hakları Saklıdır
</footer>

<script>
let cart = JSON.parse(localStorage.getItem("cart")) || [];

function updateCart(){
    document.getElementById("cartCount").innerText = cart.length;
    localStorage.setItem("cart", JSON.stringify(cart));
}

function addToCart(name, price){
    cart.push({name, price});
    updateCart();
    alert("Sepete eklendi!");
}

function showSection(type){
    let content = document.getElementById("content");
    
    if(type === "pubg"){
        content.innerHTML = `
        <div class="container">
            <div class="card">
                <h3>60 UC</h3>
                <p>₺35</p>
                <button onclick="addToCart('60 UC', 35)">Sepete Ekle</button>
            </div>
            <div class="card">
                <h3>325 UC</h3>
                <p>₺180</p>
                <button onclick="addToCart('325 UC', 180)">Sepete Ekle</button>
            </div>
            <div class="card">
                <h3>660 UC</h3>
                <p>₺350</p>
                <button onclick="addToCart('660 UC', 350)">Sepete Ekle</button>
            </div>
        </div>
        `;
    }

    if(type === "store"){
        content.innerHTML = `
        <div class="container">
            <div class="card">
                <h3>Premium Hoodie</h3>
                <p>₺799</p>
                <button onclick="addToCart('Premium Hoodie', 799)">Sepete Ekle</button>
            </div>
            <div class="card">
                <h3>Street T-Shirt</h3>
                <p>₺399</p>
                <button onclick="addToCart('Street T-Shirt', 399)">Sepete Ekle</button>
            </div>
        </div>
        `;
    }
}

function showCart(){
    let content = document.getElementById("content");
    let total = cart.reduce((sum, item) => sum + item.price, 0);
    
    let items = cart.map(item => `<p>${item.name} - ₺${item.price}</p>`).join("");
    
    content.innerHTML = `
        <div style="padding:20px;">
            <h2>Sepet</h2>
            ${items}
            <h3>Toplam: ₺${total}</h3>
            <button onclick="alert('Ödeme sistemi eklenecek')">Ödeme Yap</button>
        </div>
    `;
}

updateCart();
showSection('pubg');
</script>

</body>
</html>
