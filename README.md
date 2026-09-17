# Conversor_Temperatura
Convierte la tempreatura de °C, °F y °K
 
<!DOCTYPE html>
<html lang="es" data-theme="dark">
<head>
  <meta charset="UTF-8">

  <meta
    name="viewport"
    content="width=device-width, initial-scale=1.0"
  >

  <meta
    name="description"
    content="Calculadora moderna para convertir temperaturas entre Celsius, Fahrenheit y Kelvin."
  >

  <meta name="color-scheme" content="light dark">

  <title>TermoConvert | Conversor de temperaturas</title>

  <style>
    :root {
      --accent: #41c7ff;
      --accent-2: #5b7cff;
      --accent-rgb: 65, 199, 255;

      --bg-a: #07111f;
      --bg-b: #131b3e;

      --surface: rgba(12, 22, 42, 0.78);
      --surface-strong: rgba(21, 31, 56, 0.94);
      --surface-soft: rgba(255, 255, 255, 0.07);

      --text: #f7fbff;
      --muted: #acb9ce;
      --border: rgba(255, 255, 255, 0.13);

      --danger: #ff6b7a;
      --success: #6bf0b2;

      --shadow:
        0 30px 80px rgba(0, 0, 0, 0.42),
        0 10px 28px rgba(0, 0, 0, 0.24);

      --radius: 28px;
    }

    html[data-theme="light"] {
      --bg-a: #e8f7ff;
      --bg-b: #eef0ff;

      --surface: rgba(255, 255, 255, 0.79);
      --surface-strong: rgba(255, 255, 255, 0.95);
      --surface-soft: rgba(25, 42, 72, 0.055);

      --text: #152039;
      --muted: #5f6b80;
      --border: rgba(25, 42, 72, 0.12);

      --shadow:
        0 30px 75px rgba(52, 75, 110, 0.2),
        0 10px 26px rgba(52, 75, 110, 0.1);
    }

    * {
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      min-height: 100vh;
      margin: 0;
      overflow-x: hidden;

      color: var(--text);

      font-family:
        Inter,
        ui-sans-serif,
        system-ui,
        -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        sans-serif;

      background:
        radial-gradient(
          circle at 14% 12%,
          rgba(var(--accent-rgb), 0.25),
          transparent 30rem
        ),
        radial-gradient(
          circle at 86% 84%,
          color-mix(in srgb, var(--accent-2) 24%, transparent),
          transparent 35rem
        ),
        linear-gradient(135deg, var(--bg-a), var(--bg-b));

      transition:
        background 0.55s ease,
        color 0.35s ease;
    }

    body::before,
    body::after {
      content: "";
      position: fixed;
      z-index: -1;

      border-radius: 50%;
      filter: blur(4px);
      opacity: 0.5;

      animation: float 10s ease-in-out infinite;
    }

    body::before {
      width: 240px;
      height: 240px;

      top: 5%;
      left: -70px;

      background:
        linear-gradient(
          135deg,
          var(--accent),
          transparent
        );
    }

    body::after {
      width: 310px;
      height: 310px;

      right: -90px;
      bottom: 4%;

      background:
        linear-gradient(
          135deg,
          transparent,
          var(--accent-2)
        );

      animation-delay: -4s;
    }

    button,
    input,
    select {
      font: inherit;
    }

    button,
    select {
      cursor: pointer;
    }

    button:focus-visible,
    input:focus-visible,
    select:focus-visible {
      outline:
        3px solid
        color-mix(in srgb, var(--accent) 62%, white);

      outline-offset: 3px;
    }

    .app-shell {
      width: min(980px, calc(100% - 28px));
      margin: 0 auto;
      padding: 28px 0 48px;
    }

    .topbar {
      display: flex;
      align-items: center;
      justify-content: space-between;

      gap: 16px;
      margin-bottom: 22px;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .brand-mark {
      display: grid;
      place-items: center;

      width: 46px;
      height: 46px;

      border: 1px solid var(--border);
      border-radius: 16px;

      color: white;

      background:
        linear-gradient(
          145deg,
          var(--accent),
          var(--accent-2)
        );

      box-shadow:
        0 10px 26px rgba(var(--accent-rgb), 0.28);

      font-size: 1.35rem;

      transform: rotate(-5deg);
    }

    .brand strong {
      display: block;
      font-size: 1.08rem;
      letter-spacing: -0.02em;
    }

    .brand span {
      color: var(--muted);
      font-size: 0.78rem;
    }

    .icon-button {
      position: relative;

      display: inline-grid;
      place-items: center;

      width: 46px;
      height: 46px;

      border: 1px solid var(--border);
      border-radius: 15px;

      color: var(--text);
      background: var(--surface);

      box-shadow:
        0 8px 24px rgba(0, 0, 0, 0.08);

      transition:
        transform 0.22s ease,
        background 0.22s ease,
        border-color 0.22s ease;
    }

    .icon-button:hover {
      transform: translateY(-3px) rotate(3deg);
      border-color: var(--accent);
    }

    .icon-button:active {
      transform: scale(0.94);
    }

    .hero-card {
      position: relative;
      overflow: hidden;

      padding: clamp(22px, 4vw, 42px);

      border: 1px solid var(--border);
      border-radius: var(--radius);

      background:
        linear-gradient(
          145deg,
          var(--surface-strong),
          var(--surface)
        );

      box-shadow: var(--shadow);

      backdrop-filter: blur(24px);
      -webkit-backdrop-filter: blur(24px);

      transition:
        border-color 0.4s ease,
        box-shadow 0.4s ease;
    }

    .hero-card::before {
      content: "";

      position: absolute;

      width: 340px;
      height: 340px;

      right: -160px;
      top: -190px;

      border-radius: 50%;

      background:
        radial-gradient(
          circle,
          rgba(var(--accent-rgb), 0.35),
          transparent 68%
        );

      pointer-events: none;
    }

    .eyebrow {
      display: inline-flex;
      align-items: center;

      gap: 8px;
      margin: 0 0 10px;

      color: var(--accent);

      font-size: 0.76rem;
      font-weight: 800;
      letter-spacing: 0.16em;
      text-transform: uppercase;
    }

    h1 {
      max-width: 720px;
      margin: 0;

      font-size: clamp(2rem, 6vw, 4rem);
      line-height: 1.02;
      letter-spacing: -0.055em;
    }

    .lead {
      max-width: 650px;
      margin: 14px 0 30px;

      color: var(--muted);
      line-height: 1.65;
    }

    .converter {
      display: grid;

      grid-template-columns:
        minmax(0, 1fr)
        auto
        minmax(0, 1fr);

      align-items: stretch;
      gap: 14px;
    }

    .unit-panel {
      position: relative;
      min-width: 0;

      padding: 20px;

      border: 1px solid var(--border);
      border-radius: 22px;

      background: var(--surface-soft);

      transition:
        transform 0.25s ease,
        border-color 0.3s ease,
        background 0.3s ease;
    }

    .unit-panel:focus-within {
      transform: translateY(-3px);

      border-color:
        color-mix(
          in srgb,
          var(--accent) 65%,
          transparent
        );
    }

    .field-label {
      display: flex;
      justify-content: space-between;

      gap: 12px;
      margin-bottom: 10px;

      color: var(--muted);

      font-size: 0.82rem;
      font-weight: 700;
    }

    select {
      width: 100%;

      padding: 12px 38px 12px 13px;

      border: 1px solid var(--border);
      border-radius: 13px;

      color: var(--text);
      background: var(--surface-strong);
    }

    .input-wrap {
      position: relative;
      margin-top: 18px;
    }

    .temperature-input,
    .result-value {
      width: 100%;
      min-width: 0;

      border: 0;

      color: var(--text);
      background: transparent;

      font-size: clamp(2rem, 5vw, 3.55rem);
      font-weight: 800;
      letter-spacing: -0.05em;
    }

    .temperature-input {
      padding: 0 58px 8px 0;
      border-bottom: 2px solid var(--border);
    }

    .temperature-input::placeholder {
      color:
        color-mix(
          in srgb,
          var(--muted) 55%,
          transparent
        );
    }

    .temperature-input:focus {
      border-color: var(--accent);
      outline: none;
    }

    .unit-symbol {
      position: absolute;

      right: 0;
      bottom: 16px;

      color: var(--accent);

      font-size: 1.25rem;
      font-weight: 800;
    }

    .result-value {
      display: flex;
      align-items: center;

      min-height: 76px;
      padding: 2px 0;

      color: var(--accent);

      overflow-wrap: anywhere;

      text-shadow:
        0 0 28px rgba(var(--accent-rgb), 0.25);
    }

    .result-value.pop {
      animation: resultPop 0.38s ease;
    }

    .result-caption {
      margin: 8px 0 0;

      color: var(--muted);
      font-size: 0.82rem;
    }

    .swap-wrap {
      display: grid;
      place-items: center;
    }

    .swap-button {
      display: grid;
      place-items: center;

      width: 54px;
      height: 54px;

      border: 0;
      border-radius: 18px;

      color: white;

      background:
        linear-gradient(
          145deg,
          var(--accent),
          var(--accent-2)
        );

      box-shadow:
        0 12px 26px rgba(var(--accent-rgb), 0.28);

      font-size: 1.35rem;

      transition:
        transform 0.28s cubic-bezier(0.2, 0.8, 0.2, 1),
        filter 0.25s ease;
    }

    .swap-button:hover {
      transform: rotate(180deg) scale(1.06);
      filter: brightness(1.12);
    }

    .swap-button:active {
      transform: rotate(180deg) scale(0.92);
    }

    .message {
      min-height: 23px;
      margin: 14px 2px 0;

      color: var(--muted);
      font-size: 0.88rem;
    }

    .message.error {
      color: var(--danger);
      font-weight: 700;
    }

    .message.valid {
      color: var(--success);
    }

    .actions {
      display: flex;
      flex-wrap: wrap;

      gap: 10px;
      margin-top: 18px;
    }

    .action-button {
      display: inline-flex;
      align-items: center;
      justify-content: center;

      gap: 9px;
      min-height: 44px;
      padding: 0 17px;

      border: 1px solid var(--border);
      border-radius: 14px;

      color: var(--text);
      background: var(--surface-soft);

      font-weight: 750;

      transition:
        transform 0.2s ease,
        border-color 0.2s ease,
        background 0.2s ease;
    }

    .action-button:hover {
      transform: translateY(-2px);
      border-color: var(--accent);

      background:
        rgba(var(--accent-rgb), 0.1);
    }

    .action-button:active {
      transform: scale(0.97);
    }

    .formula-section {
      display: grid;
      grid-template-columns: 1fr 1.45fr;

      gap: 18px;
      margin-top: 20px;
      padding: 22px;

      border: 1px solid var(--border);
      border-radius: 22px;

      background: var(--surface-soft);
    }

    .formula-section h2 {
      margin: 0 0 6px;
      font-size: 1.08rem;
    }

    .formula-section p {
      margin: 0;

      color: var(--muted);

      font-size: 0.87rem;
      line-height: 1.5;
    }

    .formula-active {
      display: grid;
      place-items: center;

      min-height: 68px;
      padding: 15px;

      border-radius: 16px;

      color: var(--accent);
      background: rgba(var(--accent-rgb), 0.1);

      font-family:
        ui-monospace,
        SFMono-Regular,
        Menlo,
        Consolas,
        monospace;

      font-size: clamp(0.9rem, 2.5vw, 1.05rem);
      font-weight: 800;
      text-align: center;

      transition:
        color 0.3s ease,
        background 0.3s ease;
    }

    .all-formulas {
      display: grid;
      grid-template-columns: repeat(3, 1fr);

      gap: 10px;
      margin-top: 14px;
    }

    details {
      border: 1px solid var(--border);
      border-radius: 14px;

      background: var(--surface-soft);
    }

    summary {
      padding: 13px 14px;

      cursor: pointer;

      font-size: 0.82rem;
      font-weight: 750;
    }

    details p {
      padding: 0 14px 14px;
      font-family: ui-monospace, monospace;
    }

    .footer-note {
      margin: 18px 0 0;

      color: var(--muted);

      text-align: center;
      font-size: 0.76rem;
    }

    .sr-only {
      position: absolute;

      width: 1px;
      height: 1px;

      padding: 0;
      margin: -1px;

      overflow: hidden;

      clip: rect(0, 0, 0, 0);
      white-space: nowrap;

      border: 0;
    }

    @keyframes float {
      0%,
      100% {
        transform: translate3d(0, 0, 0);
      }

      50% {
        transform: translate3d(20px, -18px, 0);
      }
    }

    @keyframes resultPop {
      0% {
        opacity: 0.35;
        transform: translateY(8px) scale(0.96);
      }

      100% {
        opacity: 1;
        transform: none;
      }
    }

    @media (max-width: 720px) {
      .converter {
        grid-template-columns: 1fr;
      }

      .swap-wrap {
        height: 42px;
      }

      .swap-button {
        width: 50px;
        height: 50px;

        transform: rotate(90deg);
      }

      .swap-button:hover {
        transform: rotate(270deg) scale(1.06);
      }

      .formula-section {
        grid-template-columns: 1fr;
      }

      .all-formulas {
        grid-template-columns: 1fr;
      }
    }

    @media (max-width: 420px) {
      .app-shell {
        width: min(100% - 18px, 980px);
        padding-top: 16px;
      }

      .hero-card {
        padding: 19px;
        border-radius: 22px;
      }

      .unit-panel {
        padding: 16px;
      }

      .brand span {
        display: none;
      }

      .actions .action-button {
        flex: 1;
      }
    }

    @media (prefers-reduced-motion: reduce) {
      *,
      *::before,
      *::after {
        scroll-behavior: auto !important;
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
      }
    }
  </style>
</head>

<body>
  <main class="app-shell">
    <header class="topbar">
      <div class="brand" aria-label="TermoConvert">
        <div class="brand-mark" aria-hidden="true">
          ♨
        </div>

        <div>
          <strong>TermoConvert</strong>
          <span>Precisión en cada grado</span>
        </div>
      </div>

      <button
        class="icon-button"
        id="themeButton"
        type="button"
        aria-label="Cambiar a modo claro"
        title="Cambiar tema"
      >
        <span id="themeIcon" aria-hidden="true">☀️</span>
      </button>
    </header>

    <section class="hero-card" aria-labelledby="mainTitle">
      <p class="eyebrow">
        <span id="climateIcon" aria-hidden="true">❄️</span>
        Conversión instantánea
      </p>

      <h1 id="mainTitle">
        La temperatura,<br>
        en tu unidad.
      </h1>

      <p class="lead">
        Convierte entre Celsius, Fahrenheit y Kelvin mientras
        escribes, con validación automática y fórmulas
        transparentes.
      </p>

      <div class="converter">
        <section
          class="unit-panel"
          aria-labelledby="originLabel"
        >
          <label
            class="field-label"
            id="originLabel"
            for="fromUnit"
          >
            <span>Unidad inicial</span>
            <span aria-hidden="true">Entrada</span>
          </label>

          <select id="fromUnit" aria-describedby="message">
            <option value="C">Celsius (°C)</option>
            <option value="F">Fahrenheit (°F)</option>
            <option value="K">Kelvin (K)</option>
          </select>

          <div class="input-wrap">
            <label
              class="sr-only"
              for="temperatureInput"
            >
              Temperatura que deseas convertir
            </label>

            <input
              class="temperature-input"
              id="temperatureInput"
              type="text"
              inputmode="decimal"
              autocomplete="off"
              placeholder="0"
              aria-describedby="message"
              autofocus
            >

            <span
              class="unit-symbol"
              id="fromSymbol"
              aria-hidden="true"
            >
              °C
            </span>
          </div>
        </section>

        <div class="swap-wrap">
          <button
            class="swap-button"
            id="swapButton"
            type="button"
            aria-label="Intercambiar unidades"
            title="Intercambiar unidades"
          >
            ⇄
          </button>
        </div>

        <section
          class="unit-panel"
          aria-labelledby="destinationLabel"
        >
          <label
            class="field-label"
            id="destinationLabel"
            for="toUnit"
          >
            <span>Unidad final</span>
            <span aria-hidden="true">Resultado</span>
          </label>

          <select id="toUnit" aria-describedby="message">
            <option value="F">Fahrenheit (°F)</option>
            <option value="C">Celsius (°C)</option>
            <option value="K">Kelvin (K)</option>
          </select>

          <div
            class="result-value"
            id="result"
            aria-live="polite"
            aria-atomic="true"
          >
            32 °F
          </div>

          <p class="result-caption" id="resultCaption">
            Resultado de la conversión
          </p>
        </section>
      </div>

      <p
        class="message valid"
        id="message"
        role="status"
        aria-live="polite"
      >
        Introduce una temperatura para comenzar.
      </p>

      <div class="actions">
        <button
          class="action-button"
          id="resetButton"
          type="button"
        >
          <span aria-hidden="true">↺</span>
          Reiniciar
        </button>

        <button
          class="action-button"
          id="copyButton"
          type="button"
        >
          <span aria-hidden="true">⧉</span>
          Copiar resultado
        </button>
      </div>

      <section
        class="formula-section"
        aria-labelledby="formulaTitle"
      >
        <div>
          <h2 id="formulaTitle">Fórmula utilizada</h2>

          <p>
            La fórmula se actualiza según las unidades
            seleccionadas.
          </p>
        </div>

        <div class="formula-active" id="activeFormula">
          °F = (°C × 9/5) + 32
        </div>
      </section>

      <div
        class="all-formulas"
        aria-label="Referencia rápida de fórmulas"
      >
        <details>
          <summary>Desde Celsius</summary>

          <p>
            °F = (°C × 9/5) + 32
            <br>
            K = °C + 273.15
          </p>
        </details>

        <details>
          <summary>Desde Fahrenheit</summary>

          <p>
            °C = (°F − 32) × 5/9
            <br>
            K = (°F − 32) × 5/9 + 273.15
          </p>
        </details>

        <details>
          <summary>Desde Kelvin</summary>

          <p>
            °C = K − 273.15
            <br>
            °F = (K − 273.15) × 9/5 + 32
          </p>
        </details>
      </div>
    </section>

    <p class="footer-note">
      Cero absoluto: −273.15 °C, −459.67 °F o 0 K.
    </p>
  </main>

  <script>
    (() => {
      "use strict";

      const $ = (selector) => document.querySelector(selector);

      const input = $("#temperatureInput");
      const fromUnit = $("#fromUnit");
      const toUnit = $("#toUnit");
      const fromSymbol = $("#fromSymbol");
      const result = $("#result");
      const resultCaption = $("#resultCaption");
      const message = $("#message");
      const formula = $("#activeFormula");
      const climateIcon = $("#climateIcon");
      const themeButton = $("#themeButton");
      const themeIcon = $("#themeIcon");
      const root = document.documentElement;

      const units = {
        C: {
          name: "Celsius",
          symbol: "°C",
          minimum: -273.15,
          color: "#41c7ff",
          color2: "#5b7cff",
          rgb: "65, 199, 255",
          icon: "❄️"
        },

        F: {
          name: "Fahrenheit",
          symbol: "°F",
          minimum: -459.67,
          color: "#ff6b7a",
          color2: "#ff9e44",
          rgb: "255, 107, 122",
          icon: "🔥"
        },

        K: {
          name: "Kelvin",
          symbol: "K",
          minimum: 0,
          color: "#a879ff",
          color2: "#42dfc8",
          rgb: "168, 121, 255",
          icon: "✨"
        }
      };

      const formulas = {
        "C-F": "°F = (°C × 9/5) + 32",
        "C-K": "K = °C + 273.15",
        "F-C": "°C = (°F − 32) × 5/9",
        "F-K": "K = (°F − 32) × 5/9 + 273.15",
        "K-C": "°C = K − 273.15",
        "K-F": "°F = (K − 273.15) × 9/5 + 32"
      };

      function toCelsius(value, unit) {
        if (unit === "C") {
          return value;
        }

        if (unit === "F") {
          return (value - 32) * 5 / 9;
        }

        return value - 273.15;
      }

      function fromCelsius(value, unit) {
        if (unit === "C") {
          return value;
        }

        if (unit === "F") {
          return value * 9 / 5 + 32;
        }

        return value + 273.15;
      }

      function parseTemperature(raw) {
        const normalized = raw
          .trim()
          .replace(",", ".");

        if (!normalized) {
          return {
            empty: true
          };
        }

        const numberPattern =
          /^[+-]?(?:\d+(?:\.\d*)?|\.\d+)$/;

        if (!numberPattern.test(normalized)) {
          return {
            invalid: true
          };
        }

        const value = Number(normalized);

        if (!Number.isFinite(value)) {
          return {
            invalid: true
          };
        }

        return {
          value
        };
      }

      function formatNumber(value) {
        if (Math.abs(value) < 1e-12) {
          value = 0;
        }

        return new Intl.NumberFormat("es-ES", {
          maximumFractionDigits: 4,
          minimumFractionDigits: 0
        }).format(value);
      }

      function animateResult() {
        result.classList.remove("pop");

        void result.offsetWidth;

        result.classList.add("pop");
      }

      function setMessage(text, type = "") {
        message.textContent = text;
        message.className = `message ${type}`.trim();
      }

      function updateVisuals() {
        const selectedUnit = units[toUnit.value];

        root.style.setProperty(
          "--accent",
          selectedUnit.color
        );

        root.style.setProperty(
          "--accent-2",
          selectedUnit.color2
        );

        root.style.setProperty(
          "--accent-rgb",
          selectedUnit.rgb
        );

        fromSymbol.textContent =
          units[fromUnit.value].symbol;

        climateIcon.textContent =
          selectedUnit.icon;

        if (fromUnit.value === toUnit.value) {
          formula.textContent =
            `${units[toUnit.value].symbol} = ` +
            `${units[fromUnit.value].symbol}`;

          return;
        }

        formula.textContent =
          formulas[`${fromUnit.value}-${toUnit.value}`];
      }

      function convert() {
        updateVisuals();

        const parsed = parseTemperature(input.value);
        const outputUnit = units[toUnit.value];
        const inputUnit = units[fromUnit.value];

        if (parsed.empty) {
          result.textContent =
            `— ${outputUnit.symbol}`;

          resultCaption.textContent =
            "Esperando un valor";

          setMessage(
            "Introduce una temperatura para comenzar."
          );

          return;
        }

        if (parsed.invalid) {
          result.textContent =
            `— ${outputUnit.symbol}`;

          resultCaption.textContent =
            "No se pudo calcular";

          setMessage(
            "Usa únicamente un número válido, por ejemplo: -12.5",
            "error"
          );

          return;
        }

        if (parsed.value < inputUnit.minimum) {
          result.textContent =
            `— ${outputUnit.symbol}`;

          resultCaption.textContent =
            "Valor físicamente imposible";

          setMessage(
            `El mínimo posible en ${inputUnit.name} es ` +
            `${formatNumber(inputUnit.minimum)} ` +
            `${inputUnit.symbol}.`,
            "error"
          );

          return;
        }

        const valueInCelsius = toCelsius(
          parsed.value,
          fromUnit.value
        );

        const convertedValue = fromCelsius(
          valueInCelsius,
          toUnit.value
        );

        result.textContent =
          `${formatNumber(convertedValue)} ` +
          `${outputUnit.symbol}`;

        resultCaption.textContent =
          `${formatNumber(parsed.value)} ` +
          `${inputUnit.symbol} equivalen a`;

        setMessage(
          "Conversión válida y actualizada automáticamente.",
          "valid"
        );

        animateResult();
      }

      function swapUnits() {
        const previousFrom = fromUnit.value;
        const previousTo = toUnit.value;

        fromUnit.value = previousTo;
        toUnit.value = previousFrom;

        const parsed = parseTemperature(input.value);
        const previousUnit = units[previousFrom];

        const canConvertCurrentValue =
          !parsed.empty &&
          !parsed.invalid &&
          parsed.value >= previousUnit.minimum;

        if (canConvertCurrentValue) {
          const valueInCelsius = toCelsius(
            parsed.value,
            previousFrom
          );

          const convertedValue = fromCelsius(
            valueInCelsius,
            fromUnit.value
          );

          input.value = String(
            Number(convertedValue.toFixed(6))
          );
        }

        convert();
        input.focus();
      }

      function resetApplication() {
        fromUnit.value = "C";
        toUnit.value = "F";
        input.value = "";

        convert();
        input.focus();
      }

      function applyTheme(theme) {
        root.dataset.theme = theme;

        const isDark = theme === "dark";

        themeIcon.textContent =
          isDark ? "☀️" : "🌙";

        themeButton.setAttribute(
          "aria-label",
          isDark
            ? "Cambiar a modo claro"
            : "Cambiar a modo oscuro"
        );

        try {
          localStorage.setItem(
            "temperature-theme",
            theme
          );
        } catch (error) {
          console.info(
            "No fue posible guardar la preferencia de tema."
          );
        }
      }

      async function copyResult() {
        if (result.textContent.startsWith("—")) {
          setMessage(
            "Primero introduce un valor válido para copiar el resultado.",
            "error"
          );

          return;
        }

        try {
          await navigator.clipboard.writeText(
            result.textContent
          );

          setMessage(
            "Resultado copiado al portapapeles.",
            "valid"
          );
        } catch (error) {
          setMessage(
            "No fue posible copiar automáticamente en este navegador.",
            "error"
          );
        }
      }

      input.addEventListener("input", convert);

      fromUnit.addEventListener(
        "change",
        convert
      );

      toUnit.addEventListener(
        "change",
        convert
      );

      $("#swapButton").addEventListener(
        "click",
        swapUnits
      );

      $("#resetButton").addEventListener(
        "click",
        resetApplication
      );

      $("#copyButton").addEventListener(
        "click",
        copyResult
      );

      themeButton.addEventListener("click", () => {
        const newTheme =
          root.dataset.theme === "dark"
            ? "light"
            : "dark";

        applyTheme(newTheme);
      });

      let savedTheme = null;

      try {
        savedTheme = localStorage.getItem(
          "temperature-theme"
        );
      } catch (error) {
        savedTheme = null;
      }

      const systemPrefersLight =
        window.matchMedia(
          "(prefers-color-scheme: light)"
        ).matches;

      const preferredTheme =
        savedTheme ||
        (systemPrefersLight ? "light" : "dark");

      applyTheme(preferredTheme);
      convert();
    })();
  </script>
</body>
</html>
