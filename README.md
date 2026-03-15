<!DOCTYPE html>
<html lang="en">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The King Creations</title>

<style>

body{
font-family:Arial;
margin:0;
background:#f3f3f3;
}

header{
background:black;
color:gold;
padding:15px;
display:flex;
justify-content:space-between;
align-items:center;
}

.logo{
font-size:24px;
font-weight:bold;
}

.search{
width:40%;
padding:8px;
}

.cart{
background:white;
color:black;
padding:10px;
border-radius:6px;
}

.products{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
gap:20px;
padding:30px;
}

.product{
background:white;
padding:15px;
border-radius:10px;
box-shadow:0 0 10px rgba(0,0,0,0.1);
text-align:center;
}

.product img{
width:100%;
border-radius:6px;
}

button{
background:black;
color:gold;
border:none;
padding:10px;
margin-top:10px;
cursor:pointer;
}

button:hover{
background:gold;
color:black;
}

.cart-panel{
position:fixed;
right:0;
top:0;
width:300px;
height:100%;
background:white;
padding:20px;
box-shadow:-3px 0 10px rgba(0,0,0,0.2);
display:none;
overflow:auto;
}

.checkout{
background:black;
color:white;
padding:15px;
width:100%;
margin-top:10px;
}

</style>
</head>

<body>

<header>

<div class="logo">👑 The King Creations</div>

<input
class="search"
placeholder="Search products..."
onkeyup="searchProducts(this.value)"
>

<div class="cart" onclick="toggleCart()">
🛒 Cart (<span id="cart-count">0</span>)
</div>

</header>

<div class="products" id="products"></div>

<div class="cart-panel" id="cart-panel">

<h2>Your Cart</h2>

<div id="cart-items"></div>

<h3>Total: $<span id="total">0</span></h3>

<button class="checkout" onclick="checkout()">
Checkout
</button>

</div>

<script>

const products=[

{ id:1, name:"King T-Shirt", price:20, img:"https://via.placeholder.com/200"},
{ id:2, name:"King Hat", price:15, img:"https://via.placeholder.com/200"},
{ id:3, name:"Custom Art", price:50, img:"https://via.placeholder.com/200"},
{ id:4, name:"Accessories", price:25, img:"https://via.placeholder.com/200"},
{ id:5, name:"Hoodie", price:40, img:"https://via.placeholder.com/200"},
{ id:6, name:"Phone Case", price:18, img:"https://via.placeholder.com/200"}

]

let cart=[]

function renderProducts(list){

const container=document.getElementById("products")

container.innerHTML=""

list.forEach(p=>{

container.innerHTML+=`

<div class="product">

<img src="${p.img}">

<h3>${p.name}</h3>

<p>$${p.price}</p>

<button onclick="addToCart(${p.id})">Add to Cart</button>

</div>

`

})

}

renderProducts(products)

function addToCart(id){

const product=products.find(p=>p.id===id)

cart.push(product)

updateCart()

}

function updateCart(){

document.getElementById("cart-count").innerText=cart.length

let items=""

let total=0

cart.forEach(item=>{

items+=`<p>${item.name} - $${item.price}</p>`

total+=item.price

})

document.getElementById("cart-items").innerHTML=items

document.getElementById("total").innerText=total

}

function toggleCart(){

const panel=document.getElementById("cart-panel")

panel.style.display=panel.style.display==="block"?"none":"block"

}

function checkout(){

alert("Connect Stripe or PayPal for real payments!")

}

function searchProducts(text){

const filtered=products.filter(p=>

p.name.toLowerCase().includes(text.toLowerCase())

)

renderProducts(filtered)

}

</script>

</body>
</html>
