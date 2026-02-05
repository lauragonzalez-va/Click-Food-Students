# Click-Food-Students
Codigo pantalla 1:<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Click & Food - Pedido</title>
  <style>
    body {
      font-family: Arial;
      background: #f4f4f4;
      padding: 20px;
    }
    h1 {
      text-align: center;
      color: #ff6b00;
    }
    .box {
      background: white;
      padding: 20px;
      max-width: 400px;
      margin: auto;
      border-radius: 10px;
    }
    .item {
      margin: 6px 0;
    }
    button, input {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
    }
    .verde {
      color: green;
      font-weight: bold;
      text-align: center;
    }
  </style>
</head>
<body>

<h1>🍔 Click & Food</h1>

<div class="box">
  <p><b>Selecciona los alimentos:</b></p>

  <div class="item"><input type="checkbox" value="Papas de pollo"> Papas de pollo</div>
  <div class="item"><input type="checkbox" value="Agua"> Agua</div>
  <div class="item"><input type="checkbox" value="Gaseosa"> Gaseosa</div>
  <div class="item"><input type="checkbox" value="Postre"> Postre</div>
  <div class="item"><input type="checkbox" value="Fruta"> Fruta</div>
  <div class="item"><input type="checkbox" value="Palito de queso"> Palito de queso</div>

  <label>Clave (7 números):</label>
  <input type="number" id="clave">

  <button onclick="aceptar()">Aceptar</button>

  <!-- AQUÍ SALE EL NÚMERO DE PEDIDO -->
  <p id="resultado" class="verde"></p>
</div>

<script>
  function aceptar() {
    const clave = document.getElementById("clave").value;
    const checks = document.querySelectorAll("input[type='checkbox']:checked");
    const alimentos = [...checks].map(c => c.value);

    if (clave.length !== 7) {
      alert("La clave debe tener 7 números");
      return;
    }

    if (alimentos.length === 0) {
      alert("Selecciona al menos un alimento");
      return;
    }

    // contador de pedidos
    let numeroPedido = localStorage.getItem("numeroPedido");
    numeroPedido = numeroPedido ? parseInt(numeroPedido) + 1 : 1;
    localStorage.setItem("numeroPedido", numeroPedido);

    // guardar pedido
    const pedido = {
      numero: numeroPedido,
      clave: clave,
      alimentos: alimentos,
      precio: alimentos.length * 3000
    };

    localStorage.setItem("pedidoActual", JSON.stringify(pedido));

    // mostrar número de pedido
    document.getElementById("resultado").innerText =
      "Tu número de pedido es: " + numeroPedido;
  }
</script>

</body>
</html>
