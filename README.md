<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Lista de regalos</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f5f5f5;
    }

    h1 {
      margin-top: 20px;
    }

    .contenedor {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      margin-top: 30px;
    }

    .regalo {
      background-color: white;
      border: 2px solid #ccc;
      border-radius: 10px;
      width: 200px;
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
      font-size: 0.9em;
      color: #444;
      margin-top: 10px;
    }

    button.reset {
      margin-top: 30px;
      padding: 10px 20px;
      background-color: #c62828;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button.reset:hover {
      background-color: #b71c1c;
    }
  </style>
</head>
<body>

  <h1>🎁 Lista de regalos</h1>
  <p>Haz clic en un regalo para reservarlo</p>

  <div class="contenedor">
    <div class="regalo" id="regalo1" onclick="seleccionarRegalo('regalo1')">🎧 Audífonos</div>
    <div class="regalo" id="regalo2" onclick="seleccionarRegalo('regalo2')">☕ Cafetera</div>
    <div class="regalo" id="regalo3" onclick="seleccionarRegalo('regalo3')">🍳 Juego de sartenes</div>
    <div class="regalo" id="regalo4" onclick="seleccionarRegalo('regalo4')">🍷 Copas de vino</div>
    <div class="regalo" id="regalo5" onclick="seleccionarRegalo('regalo5')">🎮 Control de videojuegos</div>
  </div>

  <button class="reset" onclick="resetear()">🗑️ Borrar todas las reservas</button>

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

      const nombre = prompt("¿Quién reserva este regalo?");
      if (!nombre) return;

      regalos[id] = nombre;
      guardarRegalos(regalos);

      actualizarVista();
    }

    function actualizarVista() {
      const regalos = obtenerRegalos();

      document.querySelectorAll(".regalo").forEach(div => {
        const id = div.id;

        if (regalos[id]) {
          div.classList.add("ocupado");
          div.innerHTML = div.innerText.split("<")[0] +
            `<div class="nombre">Reservado por: ${regalos[id]}</div>`;
          div.onclick = null;
        }
      });
    }

    function resetear() {
      if (confirm("¿Seguro que quieres borrar todas las reservas?")) {
        localStorage.removeItem("regalos");
        location.reload();
      }
    }

    actualizarVista();
  </script>

</body>
</html>
