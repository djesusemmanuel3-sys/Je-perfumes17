# JE Perfumes

Catálogo en línea de JE Perfumes. Tu esencia, nuestro aroma.

Pedidos por WhatsApp: 3330284362
Instagram: @je_perfumes17
<!DOCTYPE html>
<html lang="es"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>JE Perfumes</title>
<style>
:root{--bg:#0c0b0a;--card:#171513;--tx:#f1ede4;--mut:#a69f92;--gold:#c9a45c;--line:#2c2823}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--tx);font:16px/1.5 system-ui,sans-serif;padding-bottom:96px}
header{text-align:center;padding:26px 16px 6px}
h1{font:600 30px Georgia,serif;margin:0;color:var(--gold)}
header p{margin:4px 0 0;color:var(--mut)}
.tools{position:sticky;top:0;z-index:5;background:var(--bg);padding:12px 14px;border-bottom:1px solid var(--line)}
input{width:100%;padding:11px 14px;border-radius:24px;border:1px solid var(--line);background:var(--card);color:var(--tx);font:inherit}
.chips{display:flex;gap:8px;overflow-x:auto;padding-top:10px}
.chips button{flex:none;border:1px solid var(--line);background:none;color:var(--mut);padding:6px 14px;border-radius:20px;font:inherit;cursor:pointer}
.chips button.on{border-color:var(--gold);color:var(--gold)}
.grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;padding:14px;max-width:1100px;margin:auto}
@media(min-width:700px){.grid{grid-template-columns:repeat(4,1fr)}}
.card{background:var(--card);border:1px solid var(--line);border-radius:10px;overflow:hidden;display:flex;flex-direction:column}
.card img{width:100%;aspect-ratio:4/5;object-fit:cover;display:block;background:#222}
.info{padding:10px 12px 12px;flex:1;display:flex;flex-direction:column}
.info small{color:var(--mut)}
.info b{font:600 18px/1.2 Georgia,serif;margin-bottom:8px}
.act{margin-top:auto}
.add,.send{width:100%;border:0;border-radius:8px;background:var(--gold);color:#15110a;padding:10px;font:500 15px system-ui;cursor:pointer;text-align:center;text-decoration:none;display:block}
.step{display:flex;align-items:center;justify-content:space-between;border:1px solid var(--gold);border-radius:8px}
.step button{width:42px;height:38px;border:0;background:none;color:var(--gold);font-size:20px;cursor:pointer}
.bar{position:fixed;left:14px;right:14px;bottom:14px;z-index:8;display:none}
.bar.show{display:block}
.sheet{position:fixed;inset:0;z-index:20;background:rgba(0,0,0,.6);display:none}
.sheet.open{display:flex;align-items:flex-end}
.panel{background:var(--bg);width:100%;max-width:560px;margin:auto;max-height:88%;overflow:auto;border-radius:16px 16px 0 0;padding:18px 16px}
.row{display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid var(--line)}
.row span{flex:1}.row .step{width:112px}
textarea{width:100%;height:110px;margin:10px 0;background:var(--card);color:var(--tx);border:1px solid var(--line);border-radius:8px;padding:10px;font:14px system-ui}
.send+.send{margin-top:10px;background:none;border:1px solid var(--gold);color:var(--gold)}
</style></head><body>
<header><h1>JE Perfumes</h1><p>Tu esencia, nuestro aroma</p></header>
<div class="tools"><input id="q" type="search" placeholder="Buscar perfume o marca"><div class="chips" id="chips"></div></div>
<main class="grid" id="grid"></main>
<div class="bar" id="bar"><button class="add" id="open"></button></div>
<div class="sheet" id="sheet"><div class="panel">
<h2>Tu pedido</h2>
<div id="rows"></div>
<input id="nm" placeholder="Tu nombre">
<textarea id="msg" readonly></textarea>
<a class="send" id="wa" target="_blank">Finalizar pedido por WhatsApp</a>
<a class="send" id="ig" target="_blank" href="https://ig.me/m/je_perfumes17">Finalizar pedido por Instagram</a>
<a class="send" id="close" style="margin-top:10px;background:none;color:#a69f92">Cerrar</a>
</div></div>
<script>
const P=[["pride","Lattafa","Pride Art of Universe"],["confession","Lattafa","His Confession"],["yara_tous","Lattafa","Yara Tous"],["yara_candy","Lattafa","Yara Candy"],["valentino","Valentino","Uomo Born in Roma Extradose"],["dylan","Versace","Pour Homme Dylan Blue"],["ninepm","Afnan","9pm Night Out"],["sillage","Armaf","Club de Nuit Sillage"],["cdn","Armaf","Club de Nuit Intense Man"],["aqua","Armaf","Odyssey Aqua"],["mandarin","Armaf","Odyssey Mandarin Sky"],["king","Bharara","King"],["million","Paco Rabanne","1 Million"],["phantom","Paco Rabanne","Phantom"],["hawas","Rasasi","Hawas Ice"],["nitro","Dumont Paris","Nitro Red"],["scandal","Jean Paul Gaultier","Scandal Le Parfum"],["wanted","Azzaro","The Most Wanted Eau de Parfum Intense"],["vip","Carolina Herrera","212 VIP Black"],["voyage","Nautica","Voyage"]];
const $=s=>document.querySelector(s);const cart={};let brand="Todos";
const brands=["Todos",...new Set(P.map(p=>p[1]))];
$("#chips").innerHTML=brands.map(b=>`<button data-b="${b}" class="${b==="Todos"?"on":""}">${b}</button>`).join("");
$("#chips").onclick=e=>{const b=e.target.dataset.b;if(!b)return;brand=b;document.querySelectorAll(".chips button").forEach(x=>x.classList.toggle("on",x.dataset.b===b));render()};
$("#q").oninput=render;
function ctl(k){const n=cart[k]||0;return n?`<div class="step"><button data-m="${k}">−</button><span>${n}</span><button data-p="${k}">+</button></div>`:`<button class="add" data-p="${k}">Agregar</button>`}
function render(){const t=$("#q").value.trim().toLowerCase();
const L=P.filter(p=>(brand==="Todos"||p[1]===brand)&&(p[1]+" "+p[2]).toLowerCase().includes(t));
$("#grid").innerHTML=L.map(p=>`<article class="card"><img src="fotos/${p[0]}.jpg" alt="" onerror="this.style.visibility='hidden'"><div class="info"><small>${p[1]}</small><b>${p[2]}</b><div class="act">${ctl(p[0])}</div></div></article>`).join("");
bar()}
function text(){const l=P.filter(p=>cart[p[0]]).map(p=>`• ${cart[p[0]]} x ${p[1]} ${p[2]}`);const nm=$("#nm").value.trim();return "🛍️ NUEVO PEDIDO - JE Perfumes\n"+(nm?"Cliente: "+nm+"\n":"")+"\n"+l.join("\n")+"\n\n¿Me confirman disponibilidad?"}
function link(){const m=text();$("#msg").value=m;$("#wa").href="https://wa.me/523330284362?text="+encodeURIComponent(m)}
function bar(){const n=Object.values(cart).reduce((a,b)=>a+b,0);
$("#bar").classList.toggle("show",n>0);$("#open").textContent=`Ver mi pedido (${n})`;
$("#rows").innerHTML=P.filter(p=>cart[p[0]]).map(p=>`<div class="row"><span>${p[1]} ${p[2]}</span>${ctl(p[0])}</div>`).join("");
link();if(!n)$("#sheet").classList.remove("open")}
document.addEventListener("click",e=>{const p=e.target.closest("[data-p]"),m=e.target.closest("[data-m]");
if(p){cart[p.dataset.p]=(cart[p.dataset.p]||0)+1;render()}
if(m){const k=m.dataset.m;cart[k]=(cart[k]||1)-1;if(!cart[k])delete cart[k];render()}});
$("#open").onclick=()=>$("#sheet").classList.add("open");
$("#close").onclick=()=>$("#sheet").classList.remove("open");
$("#nm").oninput=link;
$("#ig").onclick=()=>{try{navigator.clipboard.writeText($("#msg").value)}catch(_){}};
render();
</script></body></html>
