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

    p {
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
      padding: 6px;
      margin-top: 5px;
      width: 65%;
    }

    button {
      padding: 6px 10px;
      margin-top: 5px;
      cursor: pointer;
    }

    /* 🔑 SOLO se oculta el input y el botón Elegir */
    .bloqueado input,
    .bloqueado .btn-elegir {
      display: none;
    }
  </style>
</head>

<body>

  <h1>Proyecto Matrimonio</h1>
  <h2>Fase de financiamiento 💸❤️</h2>

  <p>
    Elige un regalo y escribe tu nombre para que no se repita.<br>
    Si te equivocaste, puedes corregirlo.
  </p>

  <ul>

    <!-- REGALO 1 -->
    <li id="vasos">
      <strong>Juego de vasos</strong><br>
      <span id="vasos-nombre"></span><br>

      <input type="text" id="vasos-input" placeholder="Tu nombre"><br>

      <button class="btn-elegir" onclick="elegirRegalo('vasos')">
        Elegir
      </button>

      <button onclick="borrarRegalo('vasos')">
        Me equivoqué
      </button>
    </li>

    <!-- REGALO 2 -->
    <li id="licuadora">
      <strong>Licuadora</strong><br>
      <span id="licuadora-nombre"></span><br>

      <input type="text" id="licuadora-input" placeholder="Tu nombre"><br>

      <button class="btn-elegir" onclick="elegirRegalo('licuadora')">
        Elegir
      </button>

      <button onclick="borrarRegalo('licuadora')">
        Me equivoqué
      </button>
    </li>

    <!-- REGALO 3 -->
    <li id="sartenes">
      <strong>Juego de sartenes</strong><br>
      <span id="sartenes-nombre"></span><br>

      <input type="text" id="sartenes-input" placeholder="Tu nombre"><br>

      <button class="btn-elegir" onclick="elegirRegalo('sartenes')">
        Elegir
      </button>

      <button onclick="borrarRegalo('sartenes')">
        Me equivoqué
      </button>
    </li>

  </ul>

  <!-- 🔥 FIREBASE -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getDatabase, ref, set, onValue, remove }
      from "https://www.gstatic.com/fireb
