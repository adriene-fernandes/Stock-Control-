<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Stock Control | Gestão de Estoque e Vendas</title>
<style>
:root{--navy:#142b4a;--blue:#2364a5;--red:#d94343;--bg:#f3f6fa;--ink:#1d2939;--muted:#667085;--line:#e5eaf0;--green:#16845b;--white:#fff}
*{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--ink);font:14px/1.45 Inter,Segoe UI,Arial,sans-serif}
header{background:linear-gradient(115deg,#102642,#1f568d);color:white;padding:18px 26px;display:flex;align-items:center;justify-content:space-between;gap:16px;box-shadow:0 3px 12px #10264222}
.brand{display:flex;align-items:center;gap:12px}.logo{
  width:72px;
  height:72px;
  border-radius:12px;
  overflow:hidden;
  background:#fff;
  display:flex;
  align-items:center;
  justify-content:center;
}

.logo img{
  width:100%;
  height:100%;
  object-fit:contain;
}.brand h1{font-size:20px;margin:0;letter-spacing:.3px}.brand p{margin:2px 0 0;color:#d7e6f5;font-size:12px}
header .date{font-size:12px;color:#d7e6f5;text-align:right}
.layout{display:grid;grid-template-columns:225px 1fr;min-height:calc(100vh - 78px)}
aside{background:#fff;border-right:1px solid var(--line);padding:20px 13px}
.nav-label{font-size:10px;font-weight:800;color:#98a2b3;letter-spacing:1.2px;padding:9px 12px}
nav button{width:100%;border:0;background:transparent;text-align:left;padding:12px;border-radius:9px;color:#475467;font-weight:650;cursor:pointer;margin:2px 0}
nav button:hover,nav button.active{background:#eaf2fb;color:var(--blue)}nav button span{display:inline-block;width:25px}
.aside-note{margin:28px 7px 0;padding:13px;background:#f3f7fc;border-radius:10px;color:#667085;font-size:11px}
main{padding:25px;max-width:1500px;width:100%;margin:auto}
.page-head{display:flex;justify-content:space-between;align-items:center;gap:12px;margin-bottom:20px}.page-head h2{margin:0;font-size:23px;color:var(--navy)}.page-head p{margin:4px 0 0;color:var(--muted)}
button,.btn{cursor:pointer;border:0;border-radius:8px;padding:10px 14px;font-weight:700;font-size:13px}.primary{background:var(--blue);color:#fff}.primary:hover{background:#194e85}.secondary{background:#edf2f7;color:#344054}.danger{background:#fff0f0;color:#b42318}.success{background:var(--green);color:white}
.cards{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:14px;margin-bottom:20px}.card,.panel{background:#fff;border:1px solid var(--line);border-radius:13px;padding:17px;box-shadow:0 2px 7px #162d4a08}.card .label{color:var(--muted);font-size:12px;font-weight:650}.card .value{font-size:25px;font-weight:800;color:var(--navy);margin:8px 0 3px}.card small{color:#98a2b3}.card .icon{float:right;background:#edf4fb;border-radius:9px;padding:8px}
.grid2{display:grid;grid-template-columns:1.2fr .8fr;gap:15px}.panel h3{margin:0 0 14px;color:var(--navy);font-size:15px}.panel-head{display:flex;justify-content:space-between;align-items:center;gap:10px;margin-bottom:12px}
table{width:100%;border-collapse:collapse;min-width:580px}th{text-align:left;color:#667085;font-size:11px;text-transform:uppercase;letter-spacing:.5px;background:#f8fafc;padding:11px 10px}td{padding:12px 10px;border-bottom:1px solid #eef1f5;font-size:13px}tr:last-child td{border-bottom:0}.table-wrap{overflow:auto}
.badge{display:inline-block;border-radius:30px;padding:4px 8px;font-size:11px;font-weight:750;background:#e9f7ef;color:#16734d}.badge.low{background:#fff3e8;color:#b54708}.badge.out{background:#fff0f0;color:#b42318}
.toolbar{display:flex;gap:9px;flex-wrap:wrap;margin-bottom:14px}.toolbar input,.toolbar select,.field input,.field select,.field textarea{border:1px solid #d0d5dd;border-radius:8px;padding:10px 11px;font:inherit;background:white;min-width:0}.toolbar input{flex:1;min-width:180px}
.form-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:13px}.field{display:flex;flex-direction:column;gap:5px}.field label{font-size:12px;font-weight:700;color:#475467}.field.full{grid-column:1/-1}.field input,.field select{width:100%}.actions{display:flex;gap:8px;justify-content:flex-end;margin-top:16px}
.empty{text-align:center;padding:25px;color:#98a2b3}
.statline{display:flex;justify-content:space-between;padding:9px 0;border-bottom:1px solid #eef1f5}.statline:last-child{border:0}.statline strong{color:var(--navy)}
.modal{display:none;position:fixed;inset:0;background:#10264288;z-index:5;align-items:center;justify-content:center;padding:18px}.modal.open{display:flex}.modal-box{background:white;width:min(650px,100%);max-height:92vh;overflow:auto;border-radius:15px;padding:22px;box-shadow:0 20px 60px #0003}.modal-box h3{margin:0 0 18px;color:var(--navy)}
.sale-layout{display:grid;grid-template-columns:1fr 310px;gap:15px}.sale-summary{background:#f7f9fc;border-radius:10px;padding:15px}.sale-summary .total{font-size:25px;font-weight:850;color:var(--navy)}
.toast{position:fixed;right:20px;bottom:20px;background:#142b4a;color:white;padding:12px 18px;border-radius:9px;display:none;z-index:9;box-shadow:0 8px 25px #0002}.muted{color:var(--muted)}.small{font-size:11px}
@media(max-width:900px){.layout{grid-template-columns:1fr}aside{border-right:0;border-bottom:1px solid var(--line);padding:8px}nav{display:flex;overflow:auto}nav button{white-space:nowrap;width:auto}.nav-label,.aside-note{display:none}.cards{grid-template-columns:repeat(2,1fr)}.grid2,.sale-layout{grid-template-columns:1fr}}
@media(max-width:560px){header{padding:14px}.date{display:none}main{padding:15px}.cards{gap:8px}.card{padding:12px}.card .value{font-size:20px}.form-grid{grid-template-columns:1fr}.field.full{grid-column:auto}.page-head{align-items:flex-start;flex-direction:column}}
</style>
</head>
<body>
<header>
    <div class="brand">
        <div class="logo">
            <img src="https://i.imgur.com/Gqsxsa3.png" alt="Logo">
            </div><div><h1>STOCK CONTROL</h1><p>Gestão inteligente de estoque e vendas</p></div></div><div class="date" id="today"></div></header>
        </div>
    </div>
</header>
<div class="layout">
<aside><div class="nav-label">MENU PRINCIPAL</div><nav>
<button class="active" data-page="dashboard"><span>▦</span>Visão geral</button>
<button data-page="products"><span>▣</span>Produtos</button>
<button data-page="sales"><span>🛒</span>Vendas</button>
<button data-page="movements"><span>⇄</span>Movimentações</button>
<button data-page="reports"><span>▤</span>Relatórios</button>
<button data-page="categories"><span>▧</span>Categorias</button>
</nav><div class="aside-note"><strong>Projeto acadêmico</strong><br>Protótipo demonstrativo. Os dados ficam salvos neste navegador.</div></aside>
<main id="content"></main>
</div>
<div class="modal" id="modal"><div class="modal-box" id="modalContent"></div></div><div class="toast" id="toast"></div>
<script>
const $=s=>document.querySelector(s), money=v=>Number(v||0).toLocaleString('pt-BR',{style:'currency',currency:'BRL'}), today= () => {
  const d = new Date();
  const year = d.getFullYear();
  const month = String(d.getMonth() + 1).padStart(2, '0');
  const day = String(d.getDate()).padStart(2, '0');

  return `${year}-${month}-${day}`;
};
$('#today').textContent=new Date().toLocaleDateString('pt-BR',{weekday:'long',day:'2-digit',month:'long',year:'numeric'});
let products=JSON.parse(localStorage.getItem('sc_products')||'null')||[
{id:1,name:'Cadeira plástica',category:'Utilidades',sku:'CAD001',price:35,cost:20,stock:24,min:5},
{id:2,name:'Mesa redonda',category:'Móveis',sku:'MES001',price:120,cost:78,stock:8,min:3},
{id:3,name:'Tambor 220 litros',category:'Armazenamento',sku:'TAM220',price:100,cost:65,stock:4,min:5},
{id:4,name:'Piscina 1.000 litros',category:'Lazer',sku:'PIS1000',price:1400,cost:1050,stock:2,min:1}
];
let sales=JSON.parse(localStorage.getItem('sc_sales')||'[]'), movements=JSON.parse(localStorage.getItem('sc_movements')||'[]'), page='dashboard', cart=[];
let categories=JSON.parse(localStorage.getItem('sc_categories')||'null');
if(!Array.isArray(categories)){
  categories=[...new Set(products.map(p=>p.category).filter(Boolean))];
}
function save(){
  localStorage.setItem('sc_products',JSON.stringify(products));
  localStorage.setItem('sc_sales',JSON.stringify(sales));
  localStorage.setItem('sc_movements',JSON.stringify(movements));
  localStorage.setItem('sc_categories',JSON.stringify(categories));
}
function toast(t){let el=$('#toast');el.textContent=t;el.style.display='block';setTimeout(()=>el.style.display='none',2600)}
function go(p){page=p;document.querySelectorAll('nav button').forEach(b=>b.classList.toggle('active',b.dataset.page===p));render()}
document.querySelectorAll('nav button').forEach(b=>b.onclick=()=>go(b.dataset.page));
function head(title,sub,btn=''){return `<div class="page-head"><div><h2>${title}</h2><p>${sub}</p></div>${btn}</div>`}
function render(){
  if(page==='dashboard')dashboard();
  if(page==='products')productPage();
  if(page==='sales')salesPage();
  if(page==='movements')movementPage();
  if(page==='reports')reportPage();
  if(page==='categories')categoryPage();
}
function dashboard(){let revenue=sales.filter(s=>s.date===today()).reduce((a,s)=>a+s.total,0), count=sales.filter(s=>s.date===today()).length, low=products.filter(p=>p.stock<=p.min), units=products.reduce((a,p)=>a+p.stock,0);
$('#content').innerHTML=head('Visão geral','Acompanhe os principais indicadores da loja.',`<button class="primary" onclick="go('sales')">＋ Nova venda</button>`)+
`<div class="cards"><div class="card"><span class="icon">💰</span><div class="label">Vendas de hoje</div><div class="value">${money(revenue)}</div><small>${count} venda(s) registrada(s)</small></div><div class="card"><span class="icon">📦</span><div class="label">Produtos cadastrados</div><div class="value">${products.length}</div><small>${units} unidades em estoque</small></div><div class="card"><span class="icon">⚠️</span><div class="label">Estoque baixo</div><div class="value">${low.length}</div><small>Produto(s) no limite mínimo</small></div><div class="card"><span class="icon">🧾</span><div class="label">Vendas realizadas</div><div class="value">${sales.length}</div><small>Histórico total</small></div></div>
<div class="grid2"><section class="panel"><h3>Vendas recentes</h3>${sales.length?`<div class="table-wrap"><table><thead><tr><th>Data</th><th>Itens</th><th>Pagamento</th><th>Total</th></tr></thead><tbody>${sales.slice(-5).reverse().map(s=>`<tr><td>${s.date.split('-').reverse().join('/')}</td><td>${s.items.reduce((a,i)=>a+i.qty,0)}</td><td>${s.payment}</td><td><strong>${money(s.total)}</strong></td></tr>`).join('')}</tbody></table></div>`:'<div class="empty">Nenhuma venda registrada ainda.</div>'}</section>
<section class="panel"><h3>Alertas de estoque</h3>${low.length?low.map(p=>`<div class="statline"><span>${p.name}</span><strong>${p.stock} un.</strong></div>`).join(''):'<div class="empty">Tudo certo! Nenhum alerta no momento.</div>'}<p class="small muted">O alerta é gerado quando a quantidade fica igual ou abaixo do estoque mínimo.</p></section></div>`}
function productPage(){ $('#content').innerHTML=head('Produtos','Cadastre, consulte e atualize seus produtos.',`<button class="primary" onclick="productModal()">＋ Novo produto</button>`)+
`<section class="panel"><div class="toolbar"><input id="psearch" placeholder="Buscar por nome, categoria ou código..." oninput="filterProducts()"><select id="pfilter" onchange="filterProducts()"><option value="">Todas as situações</option><option value="ok">Estoque normal</option><option value="low">Estoque baixo</option><option value="out">Sem estoque</option></select></div><div class="table-wrap"><table><thead><tr><th>Produto</th><th>Código</th><th>Categoria</th><th>Preço</th><th>Estoque</th><th>Situação</th><th>Ações</th></tr></thead><tbody id="productRows"></tbody></table></div></section>`;filterProducts()}
function filterProducts(){let q=($('#psearch')?.value||'').toLowerCase(),f=$('#pfilter')?.value||'';let list=products.filter(p=>(p.name+' '+p.category+' '+p.sku).toLowerCase().includes(q)).filter(p=>!f||(f==='out'?p.stock===0:f==='low'?p.stock>0&&p.stock<=p.min:p.stock>p.min));$('#productRows').innerHTML=list.length?list.map(p=>`<tr><td><strong>${p.name}</strong></td><td>${p.sku||'—'}</td><td>${p.category||'—'}</td><td>${money(p.price)}</td><td>${p.stock}</td><td><span class="badge ${p.stock===0?'out':p.stock<=p.min?'low':''}">${p.stock===0?'Sem estoque':p.stock<=p.min?'Estoque baixo':'Normal'}</span></td><td><button class="secondary" onclick="productModal(${p.id})">Editar</button> <button class="danger" onclick="deleteProduct(${p.id})">Excluir</button></td></tr>`).join(''):'<tr><td colspan="7" class="empty">Nenhum produto encontrado.</td></tr>'}
function productModal(id){let p=products.find(x=>x.id===id)||{name:'',category:'',sku:'',price:'',cost:'',stock:0,min:0};openModal(`<h3>${id?'Editar produto':'Cadastrar produto'}</h3><form id="productForm"><div class="form-grid"><div class="field"><label>Nome do produto *</label><input name="name" required value="${p.name}"></div><div class="field"><label>Código / SKU</label><inpu<div class="field">
  <label>Categoria</label>
  <select name="category">
    <option value="">Selecione uma categoria</option>
    ${categories.map(c=>`
      <option value="${c}" ${p.category===c?'selected':''}>
        ${c}
      </option>
    `).join('')}
  </select>
</div>t name="sku" value="${p.sku}"></div><div class="field"><label>Preço de venda (R$) *</label><input name="price" type="number" min="0" step=".01" required value="${p.price}"></div><div class="field"><label>Custo (R$)</label><input name="cost" type="number" min="0" step=".01" value="${p.cost}"></div><div class="field"><label>Quantidade em estoque *</label><input name="stock" type="number" min="0" required value="${p.stock}"></div><div class="field"><label>Estoque mínimo</label><input name="min" type="number" min="0" value="${p.min}"></div></div><div class="actions"><button type="button" class="secondary" onclick="closeModal()">Cancelar</button><button class="primary">Salvar produto</button></div></form>`);
$('#productForm').onsubmit=e=>{e.preventDefault();let d=Object.fromEntries(new FormData(e.target));d.price=+d.price;d.cost=+d.cost;d.stock=+d.stock;d.min=+d.min;if(id)products=products.map(x=>x.id===id?{...x,...d}:x);else products.push({id:Date.now(),...d});save();closeModal();productPage();toast('Produto salvo com sucesso!')}}
function deleteProduct(id){if(confirm('Deseja excluir este produto?')){products=products.filter(p=>p.id!==id);save();productPage();toast('Produto excluído.')}}
function salesPage(){cart=[];$('#content').innerHTML=head('Nova venda','Adicione produtos ao carrinho, escolha o pagamento e finalize.')+
`<div class="sale-layout"><section class="panel"><h3>Adicionar produtos</h3><div class="toolbar"><input id="ssearch" placeholder="Buscar produto..." oninput="renderSaleProducts()"></div><div class="table-wrap"><table><thead><tr><th>Produto</th><th>Disponível</th><th>Preço</th><th></th></tr></thead><tbody id="saleProducts"></tbody></table></div></section><section class="panel"><h3>Resumo da venda</h3><div id="cartRows" class="empty">Seu carrinho está vazio.</div><div class="sale-summary"><div class="statline"><span>Subtotal</span><strong id="subtotal">${money(0)}</strong></div><div class="statline"><span>Desconto (R$)</span><input id="discount" type="number" min="0" step=".01" value="0" style="width:95px;padding:5px" oninput="updateCart()"></div><div class="statline"><span>Total</span><strong class="total" id="total">${money(0)}</strong></div><div class="field" style="margin-top:12px"><label>Forma de pagamento *</label><select id="payment"><option>Dinheiro</option><option>Pix</option><option>Débito</option><option>Crédito</option></select></div><div class="field" style="margin-top:10px"><label>Cliente (opcional)</label><input id="customer" placeholder="Nome do cliente"></div><button class="success" style="width:100%;margin-top:14px" onclick="finishSale()">Finalizar venda</button></div></section></div>`;renderSaleProducts();updateCart()}
function renderSaleProducts(){let q=($('#ssearch')?.value||'').toLowerCase();let list=products.filter(p=>p.name.toLowerCase().includes(q)&&p.stock>0);$('#saleProducts').innerHTML=list.length?list.map(p=>`<tr><td>${p.name}</td><td>${p.stock}</td><td>${money(p.price)}</td><td><button class="primary" onclick="addCart(${p.id})">Adicionar</button></td></tr>`).join(''):'<tr><td colspan="4" class="empty">Nenhum produto disponível.</td></tr>'}
function addCart(id){let p=products.find(x=>x.id===id),item=cart.find(x=>x.id===id);if(item){if(item.qty>=p.stock)return toast('Quantidade maior que o estoque disponível.');item.qty++}else cart.push({id,qty:1});updateCart()}
function updateCart(){let box=$('#cartRows');if(!box)return;box.innerHTML=cart.length?cart.map(i=>{let p=products.find(x=>x.id===i.id);return `<div class="statline"><span>${p.name}<br><small class="muted">${money(p.price)} × ${i.qty}</small></span><span><button class="secondary" onclick="changeQty(${i.id},-1)">−</button> <button class="secondary" onclick="changeQty(${i.id},1)">+</button></span></div>`}).join(''):'<div class="empty">Seu carrinho está vazio.</div>';let sub=cart.reduce((a,i)=>a+products.find(p=>p.id===i.id).price*i.qty,0),disc=Math.max(0,+($('#discount')?.value||0)),total=Math.max(0,sub-disc);$('#subtotal').textContent=money(sub);$('#total').textContent=money(total)}
function changeQty(id,n){let i=cart.find(x=>x.id===id),p=products.find(x=>x.id===id);if(n>0&&i.qty>=p.stock)return toast('Estoque insuficiente.');i.qty+=n;if(i.qty<=0)cart=cart.filter(x=>x.id!==id);updateCart()}
function finishSale(){if(!cart.length)return toast('Adicione pelo menos um produto.');for(let i of cart){if(i.qty>products.find(p=>p.id===i.id).stock)return toast('Estoque insuficiente para '+products.find(p=>p.id===i.id).name)}let subtotal=cart.reduce((a,i)=>a+products.find(p=>p.id===i.id).price*i.qty,0),discount=Math.max(0,+$('#discount').value||0);if(discount>subtotal)return toast('O desconto não pode ser maior que o subtotal.');let sale={id:Date.now(),date:today(),customer:$('#customer').value,payment:$('#payment').value,items:cart.map(i=>({name:products.find(p=>p.id===i.id).name,qty:i.qty,price:products.find(p=>p.id===i.id).price})),subtotal,discount,total:subtotal-discount};cart.forEach(i=>{let p=products.find(p=>p.id===i.id);p.stock-=i.qty;movements.push({date:today(),product:p.name,type:'Saída por venda',qty:i.qty,detail:'Venda #'+sale.id})});sales.push(sale);save();cart=[];go('dashboard');toast('Venda finalizada e estoque atualizado!')}
function movementPage(){$('#content').innerHTML=head('Movimentações de estoque','Registre entradas, perdas ou ajustes de quantidade.',`<button class="primary" onclick="movementModal()">＋ Nova movimentação</button>`)+`<section class="panel"><div class="table-wrap"><table><thead><tr><th>Data</th><th>Produto</th><th>Tipo</th><th>Quantidade</th><th>Detalhes</th></tr></thead><tbody>${movements.length?movements.slice().reverse().map(m=>`<tr><td>${m.date.split('-').reverse().join('/')}</td><td>${m.product}</td><td>${m.type}</td><td>${m.qty}</td><td>${m.detail||'—'}</td></tr>`).join(''):'<tr><td colspan="5" class="empty">Nenhuma movimentação registrada.</td></tr>'}</tbody></table></div></section>`}
function movementModal(){if(!products.length)return toast('Cadastre um produto primeiro.');openModal(`<h3>Nova movimentação</h3><form id="moveForm"><div class="form-grid"><div class="field full"><label>Produto *</label><select name="id">${products.map(p=>`<option value="${p.id}">${p.name} (estoque: ${p.stock})</option>`).join('')}</select></div><div class="field"><label>Tipo *</label><select name="type"><option>Entrada</option><option>Saída / perda</option><option>Ajuste</option></select></div><div class="field"><label>Quantidade *</label><input name="qty" type="number" min="1" required></div><div class="field full"><label>Observação</label><input name="detail" placeholder="Ex.: compra de fornecedor, avaria..."></div></div><div class="actions"><button type="button" class="secondary" onclick="closeModal()">Cancelar</button><button class="primary">Salvar movimentação</button></div></form>`);$('#moveForm').onsubmit=e=>{e.preventDefault();let d=Object.fromEntries(new FormData(e.target)),p=products.find(x=>x.id==d.id),qty=+d.qty;if(d.type==='Saída / perda'&&qty>p.stock)return toast('Quantidade maior que o estoque.');if(d.type==='Entrada')p.stock+=qty;else if(d.type==='Saída / perda')p.stock-=qty;else p.stock=qty;movements.push({date:today(),product:p.name,type:d.type,qty,detail:d.detail});save();closeModal();movementPage();toast('Estoque atualizado!')}}
function reportPage(){let total=sales.reduce((a,s)=>a+s.total,0),byPay=['Dinheiro','Pix','Débito','Crédito'].map(k=>({k,v:sales.filter(s=>s.payment===k).reduce((a,s)=>a+s.total,0),n:sales.filter(s=>s.payment===k).length}));$('#content').innerHTML=head('Relatórios','Resumo das vendas e posição atual do estoque.',`<button class="secondary" onclick="exportCSV()">⇩ Exportar vendas CSV</button>`)+`<div class="cards"><div class="card"><div class="label">Faturamento acumulado</div><div class="value">${money(total)}</div><small>Vendas registradas</small></div><div class="card"><div class="label">Quantidade de vendas</div><div class="value">${sales.length}</div><small>Transações concluídas</small></div><div class="card"><div class="label">Valor médio por venda</div><div class="value">${money(sales.length?total/sales.length:0)}</div><small>Ticket médio</small></div><div class="card"><div class="label">Valor em estoque (custo)</div><div class="value">${money(products.reduce((a,p)=>a+p.cost*p.stock,0))}</div><small>Estimativa pelo custo cadastrado</small></div></div><div class="grid2"><section class="panel"><h3>Vendas por forma de pagamento</h3>${byPay.map(x=>`<div class="statline"><span>${x.k} <small class="muted">(${x.n} venda(s))</small></span><strong>${money(x.v)}</strong></div>`).join('')}</section><section class="panel"><h3>Posição do estoque</h3><div class="statline"><span>Total de produtos cadastrados</span><strong>${products.length}</strong></div><div class="statline"><span>Unidades disponíveis</span><strong>${products.reduce((a,p)=>a+p.stock,0)}</strong></div><div class="statline"><span>Produtos com estoque baixo</span><strong>${products.filter(p=>p.stock<=p.min).length}</strong></div><div class="statline"><span>Valor potencial de venda</span><strong>${money(products.reduce((a,p)=>a+p.price*p.stock,0))}</strong></div></section></div><p class="small muted" style="margin-top:14px">Relatórios calculados com base nos registros salvos neste navegador.</p>`}

function categoryPage(){

  let rows=categories.length ? categories.map((c,index)=>{

    let count=products.filter(p=>p.category===c).length;

    return `
      <tr>
        <td><strong>${c}</strong></td>
        <td>${count} produto(s)</td>
        <td>
          ${count>0
            ? '<span class="badge low">Em utilização</span>'
            : '<span class="badge">Disponível para exclusão</span>'}
        </td>
        <td>
          <button class="secondary" onclick="categoryModal(${index})">Editar</button>
          <button class="danger" onclick="deleteCategory(${index})">Excluir</button>
        </td>
      </tr>
    `;
  }).join('') :
  '<tr><td colspan="4" class="empty">Nenhuma categoria cadastrada.</td></tr>';

  $('#content').innerHTML =
    head('Categorias','Cadastre e organize as categorias dos seus produtos.',
      `<button class="primary" onclick="categoryModal()">＋ Nova categoria</button>`) +

    `<section class="panel">
      <div class="panel-head">
        <h3>Categorias cadastradas</h3>
        <span class="muted small">${categories.length} categoria(s)</span>
      </div>

      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th>Categoria</th>
              <th>Produtos vinculados</th>
              <th>Situação</th>
              <th>Ações</th>
            </tr>
          </thead>
          <tbody>${rows}</tbody>
        </table>
      </div>
    </section>`;
}


function categoryModal(index){

  let editing=index!==undefined;
  let oldName=editing ? categories[index] : '';

  openModal(`
    <h3>${editing?'Editar categoria':'Cadastrar categoria'}</h3>

    <form id="categoryForm">
      <div class="field">
        <label>Nome da categoria *</label>
        <input name="name" required maxlength="60"
          placeholder="Ex.: Eletrônicos"
          value="${oldName}">
      </div>

      <div class="actions">
        <button type="button" class="secondary"
          onclick="closeModal()">Cancelar</button>
        <button class="primary">
          ${editing?'Salvar alterações':'Cadastrar categoria'}
        </button>
      </div>
    </form>
  `);

  $('#categoryForm').onsubmit=e=>{
    e.preventDefault();

    let name=new FormData(e.target).get('name').trim();

    if(!name) return toast('Informe o nome da categoria.');

    let duplicate=categories.some((c,i)=>
      c.toLowerCase()===name.toLowerCase() && i!==index
    );

    if(duplicate)
      return toast('Essa categoria já está cadastrada.');

    if(editing){

      categories[index]=name;

      // Atualiza os produtos que utilizavam a categoria antiga
      products=products.map(p=>
        p.category===oldName ? {...p,category:name} : p
      );

    }else{

      categories.push(name);

    }

    save();
    closeModal();
    categoryPage();

    toast(editing
      ? 'Categoria atualizada com sucesso!'
      : 'Categoria cadastrada com sucesso!');
  };
}


function deleteCategory(index){

  let category=categories[index];

  let linkedProducts=products.filter(p=>
    p.category===category
  );

  // Bloqueia a exclusão se houver produtos vinculados
  if(linkedProducts.length>0){

    alert(
      'Não é possível excluir esta categoria!\n\n' +
      'Categoria: '+category+'\n' +
      'Produtos vinculados: '+linkedProducts.length+'\n\n' +
      'Altere a categoria dos produtos antes de excluí-la.'
    );

    return;
  }

  if(confirm('Deseja realmente excluir a categoria "'+category+'"?')){

    categories.splice(index,1);

    save();
    categoryPage();

    toast('Categoria excluída com sucesso!');
  }
}
function exportCSV(){let rows=[['ID','Data','Cliente','Pagamento','Subtotal','Desconto','Total','Itens'],...sales.map(s=>[s.id,s.date,s.customer,s.payment,s.subtotal,s.discount,s.total,s.items.map(i=>i.name+' x'+i.qty).join('; ')])];let csv=rows.map(r=>r.map(v=>'"'+String(v??'').replaceAll('"','""')+'"').join(';')).join('\n'),a=document.createElement('a');a.href=URL.createObjectURL(new Blob(['\ufeff'+csv],{type:'text/csv;charset=utf-8;'}));a.download='relatorio-vendas-stock-control.csv';a.click();URL.revokeObjectURL(a.href)}
function openModal(content){$('#modalContent').innerHTML=content;$('#modal').classList.add('open')}function closeModal(){$('#modal').classList.remove('open')}$('#modal').addEventListener('click',e=>{if(e.target.id==='modal')closeModal()});
render();
</script>
</body>
</html>
