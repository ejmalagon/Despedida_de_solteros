<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Proyecto Matrimonio: fase de financiamiento 🎉</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      text-align: center;
      margin: 0;
      padding: 0;
    }

    header {
      background-color: #222;
      color: white;
      padding: 20px;
    }

    .foto {
      margin-top: 20px;
    }

    .foto img {
      max-width: 300px;
      border-radius: 15px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
    }

    h2 {
      margin-top: 30px;
    }

    .contenedor {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      margin: 20px;
    }

    .regalo {
      background-color: white;
      border: 2px solid #ccc;
      border-radius: 10px;
      width: 220px;
      padding: 15px;
      margin: 10px;
      cursor: pointer;
      transition: 0.3s;
    }

    .regalo:hover {
      background-color: #e8f0ff;
    }

    .ocupado {
      background-color: #ddd;
      border-color: #999;
      cursor: not-allowed;
    }

    .ocupado:hover {
      background-color: #ddd;
    }

    .nombre {
      margin-top: 10px;
      font-size: 0.9em;
      color: #444;
    }

    footer {
      margin: 30px;
      font-size: 0.9em;
      color: #666;
    }
  </style>
</head>
<body>

  <header>
    <h1>🎉 Despedida de Soltero 🎉</h1>
    <p>¡Celebremos a los futuros esposos!</p>
  </header>

  <div class="foto">
    <img src="foto-amigos.jpg" alt="Los futuros esposos">
  </div>

  <h2>🎁 Lista de regalos</h2>
  <p>Haz clic en un regalo para reservarlo (no se repetirá)</p>

  <div class="contenedor">
    <div class="regalo" id="regalo1" onclick="seleccionarRegalo('regalo1')">🎧 Audífonos</div>
    <div class="regalo" id="regalo2" onclick="seleccionarRegalo('regalo2')">☕ Cafetera</div>
    <div class="regalo" id="regalo3" onclick="seleccionarRegalo('regalo3')">🍳 Juego de sartenes</div>
    <div class="regalo" id="regalo4" onclick="seleccionarRegalo('regalo4')">🍷 Copas de vino</div>
    <div class="regalo" id="regalo5" onclick="seleccionarRegalo('regalo5')">🎮 Control de videojuegos</div>
  </div>

  <footer>
    Hecho con ❤️ para una gran celebración
  </footer>

  <script>
    function obtenerRegalos() {
      return JSON.parse(localStorage.getItem("regalos")) || {};
    }

    function guardarRegalos(regalos) {
      localStorage.setItem("regalos", JSON.stringify(regalos));
    }

    function seleccionarRegalo(id) {
      const regalos = obtenerRegalos();

      if (regalos[id]) {
        alert("Este regalo ya fue reservado 🎁");
        return;
      }

      const nombre = prompt("¿Quién va a regalar esto?");
      if (!nombre) return;

      regalos[id] = nombre;
      guardarRegalos(regalos);
      actualizarVista();
    }

    function actualizarVista() {
      const regalos = obtenerRegalos();

      document.querySelectorAll(".regalo").forEach(div => {
        const id = div.id;
        const texto = div.innerText.split("\n")[0];

        if (regalos[id]) {
          div.classList.add("ocupado");
          div.innerHTML = `${texto}<div class="nombre">Reservado por: ${regalos[id]}</div>`;
          div.onclick = null;
        }
      });
    }

    actualizarVista();
  </script>

</body>
</html>
