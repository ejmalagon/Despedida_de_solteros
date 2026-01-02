<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Proyecto Matrimonio: fase de financiamiento</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 20px;
    }

    h1, h2 {
      text-align: center;
    }

    ul {
      list-style: none;
      padding: 0;
      max-width: 600px;
      margin: auto;
    }

    li {
      background: white;
      margin-bottom: 15px;
      padding: 15px;
      border-radius: 8px;
    }

    .elegido {
      color: green;
      font-weight: bold;
    }

    input {
      padding: 5px;
      margin-top: 5px;
      width: 60%;
    }

    button {
      padding: 6px 10px;
      margin-top: 5px;
      cursor: pointer;
    }

    .bloqueado button,
    .bloqueado input {
      display: none;
    }
  </style>
</head>

<body>

  <h1>Proyecto Matrimonio</h1>
  <h2>Fase de financiamiento 💸❤️</h2>

  <p style="text-align:center">
    Elige un regalo y escribe tu nombre para que no se repita.<br>
    Si te equivocaste, puedes borrar tu selección.
  </p>

  <ul>

    <!-- REGALO 1 -->
    <li id="vasos">
      <strong>Juego de vasos</strong><br>
      <span id="vasos-nombre"></span><br>

      <input type="text" id="vasos-input" placeholder="Tu nombre">
      <br>

      <button onclick="elegirRegalo('vasos')">Elegir</button>
      <button onclick="borrarRegalo('vasos')">Me equivoqué</button>
    </li>

    <!-- REGALO 2 -->
    <li id="licuadora">
      <strong>Licuadora</strong><br>
      <span id="licuadora-nombre"></span><br>

      <input type="text" id="licuadora-input" placeholder="Tu nombre">
      <br>

      <button onclick="elegirRegalo('licuadora')">Elegir</button>
      <button onclick="borrarRegalo('licuadora')">Me equivoqué</button>
    </li>

    <!-- REGALO 3 -->
    <li id="sartenes">
      <strong>Juego de sartenes</strong><br>
      <span id="sartenes-nombre"></span><br>

      <input type="text" id="sartenes-input" placeholder="Tu nombre">
      <br>

      <button onclick="elegirRegalo('sartenes')">Elegir</button>
      <button onclick="borrarRegalo('sartenes')">Me equivoqué</button>
    </li>

  </ul>

  <!-- FIREBASE -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getDatabase, ref, set, onValue, remove } 
      from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

    const firebaseConfig = {
      apiKey: "AIzaSyBBJwB7goplMb2WJpBvJU5rsvoueD84glg",
      authDomain: "despedida-ba71a.firebaseapp.com",
      databaseURL: "https://despedida-ba71a-default-rtdb.firebaseio.com",
      projectId: "despedida-ba71a",
      storageBucket: "despedida-ba71a.firebasestorage.app",
      messagingSenderId: "30414791076",
      appId: "1:30414791076:web:08d0d7494477ca5f912131",
      measurementId: "G-GY9J0H7BW8"
    };

    const app = initializeApp(firebaseConfig);
    const db = getDatabase(app);

    // Elegir regalo
    window.elegirRegalo = function(id) {
      const input = document.getElementById(id + "-input");
      const nombre = input.value.trim();

      if (nombre === "") {
        alert("Por favor escribe tu nombre");
        return;
      }

      set(ref(db, "regalos/" + id), {
        nombre: nombre
      });
    };

    // Borrar regalo
    window.borrarRegalo = function(id) {
      remove(ref(db, "regalos/" + id));
    };

    // Escuchar cambios en tiempo real
    onValue(ref(db, "regalos"), (snapshot) => {
      const data = snapshot.val() || {};

      document.querySelectorAll("li").forEach(li => {
        li.classList.remove("bloqueado");
        const span = li.querySelector("span");
        if (span) span.innerText = "";
      });

      for (let id in data) {
        const li = document.getElementById(id);
        const span = document.getElementById(id + "-nombre");

        if (li && span) {
          span.innerText = "Elegido por: " + data[id].nombre;
          span.className = "elegido";
          li.classList.add("bloqueado");
        }
      }
    });
  </script>

</body>
</html>
