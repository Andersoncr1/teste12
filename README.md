<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Painel de Gastos</title>
  <style>
    body{
      margin:0;
      font-family: Arial, Helvetica, sans-serif;
      background:linear-gradient(180deg,#0a3a66,#041f3a);
      color:#fff;
    }
    header{
      text-align:center;
      padding:30px 15px;
      background:#031629;
    }
    header h1{margin:0;font-size:1.8em;}
    header p{opacity:0.8;}
    .container{
      max-width:1000px;
      margin:auto;
      padding:20px;
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(300px,1fr));
      gap:20px;
    }
    .card{
      background:#0e2f4f;
      border-radius:16px;
      padding:20px;
      box-shadow:0 10px 25px rgba(0,0,0,0.4);
    }
    .card h2{text-align:center;margin-top:0;}
    label{display:block;margin-top:10px;font-size:0.9em;}
    input{
      width:100%;
      padding:10px;
      border-radius:10px;
      border:none;
      margin-top:5px;
    }
    button{
      width:100%;
      margin-top:15px;
      padding:12px;
      border:none;
      border-radius:12px;
      font-weight:bold;
      cursor:pointer;
      background:#00c2ff;
      color:#002033;
    }
    button:hover{background:#00e0ff;}
    ul{list-style:none;padding:0;margin-top:15px;}
    li{
      background:#08223b;
      margin-bottom:8px;
      padding:10px;
      border-radius:10px;
      display:flex;
      justify-content:space-between;
      font-size:0.9em;
    }
    .total{
      margin-top:15px;
      font-weight:bold;
      text-align:right;
    }
  </style>
</head>
<body>

<header>
  <h1>Painel de Gastos</h1>
  <p>Controle simples e separado</p>
</header>

<div class="container">

  <div class="card">
    <h2>Anderson</h2>
    <label>Descrição</label>
    <input type="text" id="descA" placeholder="Ex: Mercado">
    <label>Valor (R$)</label>
    <input type="number" id="valorA" placeholder="0.00">
    <button onclick="addGasto('A')">Adicionar gasto</button>
    <ul id="listaA"></ul>
    <div class="total">Total: R$ <span id="totalA">0.00</span></div>
  </div>

  <div class="card">
    <h2>Carla</h2>
    <label>Descrição</label>
    <input type="text" id="descC" placeholder="Ex: Farmácia">
    <label>Valor (R$)</label>
    <input type="number" id="valorC" placeholder="0.00">
    <button onclick="addGasto('C')">Adicionar gasto</button>
    <ul id="listaC"></ul>
    <div class="total">Total: R$ <span id="totalC">0.00</span></div>
  </div>

</div>

<script>
  let totalA = 0;
  let totalC = 0;

  function addGasto(tipo){
    if(tipo === 'A'){
      const desc = descA.value;
      const valor = parseFloat(valorA.value);
      if(!desc || !valor) return;
      totalA += valor;
      listaA.innerHTML += `<li><span contenteditable="true">${desc}</span><span contenteditable="true" oninput="recalcular('${tipo}')">R$ ${valor.toFixed(2)}</span></li>`;
      totalAEl.textContent = totalA.toFixed(2);
      descA.value = '';
      valorA.value = '';
    }
    if(tipo === 'C'){
      const desc = descC.value;
      const valor = parseFloat(valorC.value);
      if(!desc || !valor) return;
      totalC += valor;
      listaC.innerHTML += `<li><span contenteditable="true">${desc}</span><span contenteditable="true" oninput="recalcular('${tipo}')">R$ ${valor.toFixed(2)}</span></li>`;
      totalCEl.textContent = totalC.toFixed(2);
      descC.value = '';
      valorC.value = '';
    }
  }

  const totalAEl = document.getElementById('totalA');
  const totalCEl = document.getElementById('totalC');
