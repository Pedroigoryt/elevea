<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculadora de Elevador de Grãos</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      background-color: #f7f7f7;
      flex-direction: column;
    }

    .calculator-container {
      background: #fff;
      padding: 20px;
      border-radius: 5px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      margin-top: 20px;
      text-align: center;
    }

    .calculator-container h1 {
      color: #333;
      text-align: center;
    }

    .calculator-container label {
      display: block;
      margin-top: 10px;
      margin-bottom: 5px;
      font-weight: bold;
    }

    .calculator-container input[type="number"],
    .calculator-container select {
      width: 100%;
      padding: 8px;
      margin-bottom: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }

    .calculator-container button {
      background-color: #007BFF;
      color: white;
      padding: 10px 15px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }

    .calculator-container button:hover {
      background-color: #0056b3;
    }

    .result {
      margin-top: 20px;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
    }

    .card {
      background: #e7f3ff;
      padding: 15px;
      border: 1px solid #007BFF;
      border-radius: 5px;
      text-align: center;
    }

    .card i {
      font-size: 2em;
      margin-bottom: 10px;
    }

    .result .card p strong {
      color: #007BFF;
      font-size: 1.2em;
    }

    .calculator-container header img {
      display: block;
      margin-left: auto;
      margin-right: auto;
      width: 300px;
    }

    /* Media queries para responsividade */
    @media (max-width: 768px) {
      .calculator-container {
        padding: 20px;
      }

      input[type="text"],
      input[type="password"] {
        padding: 8px;
      }

      h1 {
        font-size: 1.8em;
      }

      .card {
        padding: 10px;
      }

      .card i {
        font-size: 1.5em;
      }

      .result .card p strong {
        font-size: 1em;
      }
    }

    @media (max-width: 480px) {
      .result {
        grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      }

      h1 {
        font-size: 1.5em;
      }
    }
  </style>
</head>
<body>
  <div class="calculator-container">
    <header>
      <img src="https://i.postimg.cc/hGCzXCRT/imagem-2024-12-11-091240921.png" alt="Imagem de Cabeçalho">
    </header>

    <h1>Calculadora de Dimensionamento do Elevador de Grãos</h1>
    <form id="elevatorForm">
      <label for="desiredHeight">Altura Total Desejada (metros):</label>
      <input type="number" id="desiredHeight" name="desiredHeight" step="0.01" required>

      <label for="capacity">Capacidade do Elevador (t/h):</label>
      <input type="number" id="capacity" name="capacity" step="0.01" required>

      <label for="grainType">Tipo de Grão:</label>
      <select id="grainType" name="grainType">
        <option value="soja">Soja</option>
        <option value="milho">Milho</option>
        <option value="trigo">Trigo</option>
        <option value="arroz">Arroz</option>
        <option value="cevada">Cevada</option>
        <option value="aveia">Aveia</option>
        <option value="sorgo">Sorgo</option>
        <option value="girassol">Girassol</option>
        <option value="algodao">Algodão em caroço</option>
        <option value="amendoim">Amendoim</option>
      </select>

      <label for="elevatorModel">Modelo do Elevador:</label>
      <select id="elevatorModel" name="elevatorModel">
        <option value="EA0">EA0</option>
        <option value="EA1">EA1</option>
        <option value="EA2">EA2</option>
        <option value="EA3">EA3</option>
        <option value="EA4">EA4</option>
      </select>

      <button type="button" onclick="calculateConfiguration()">Calcular Dimensionamento</button>
    </form>

    <div id="result" class="result">
      </div>
  </div>

  <script>
    function calculateConfiguration() {
      // Obtém os valores dos campos do formulário
      const desiredHeight = parseFloat(document.getElementById('desiredHeight').value);
      const capacity = parseFloat(document.getElementById('capacity').value);
      const grainType = document.getElementById('grainType').value;
      const elevatorModel = document.getElementById('elevatorModel').value;

      // Define a densidade do grão
      let grainDensity;
      switch (grainType) {
        case 'soja':  grainDensity = 790; break;
        case 'milho': grainDensity = 720; break;
        case 'trigo': grainDensity = 780; break;
        case 'arroz': grainDensity = 800; break;
        case 'cevada': grainDensity = 650; break;
        case 'aveia': grainDensity = 530; break;
        case 'sorgo': grainDensity = 740; break;
        case 'girassol': grainDensity = 350; break;
        case 'algodao': grainDensity = 650; break;
        case 'amendoim': grainDensity = 450; break;
        default: grainDensity = 750; // Valor padrão
      }

      // Define a velocidade da correia, espaçamento entre canecas e diâmetro do tambor
      // com base no modelo do elevador
      let beltSpeed, bucketSpacing, drumDiameter, baseThickness;

      // Lógica para definir beltSpeed, bucketSpacing, drumDiameter e baseThickness com base no modelo do elevador (substitua os valores abaixo pelos valores corretos)
      if (elevatorModel === 'EA0') {
        beltSpeed = 1.5;
        bucketSpacing = 20;
        drumDiameter = 200;
        baseThickness = 3.0; // Espessura da base para EA0
      } else if (elevatorModel === 'EA1') {
        beltSpeed = 1.5;
        bucketSpacing = 25;
        drumDiameter = 250;
        baseThickness = 4.0; // Espessura da base para EA1
      } else if (elevatorModel === 'EA2') {
        beltSpeed = 2.0;
        bucketSpacing = 25;
        drumDiameter = 315;
        baseThickness = 4.0; // Espessura da base para EA2
      } else if (elevatorModel === 'EA3') {
        beltSpeed = 2.0;
        bucketSpacing = 30;
        drumDiameter = 400;
        baseThickness = 4.0; // Espessura da base para EA3
      } else if (elevatorModel === 'EA4') {
        beltSpeed = 2.5;
        bucketSpacing = 30;
        drumDiameter = 500;
        baseThickness = 4.75; // Espessura da base para EA4
      }

      // Calcula as seções de calhas
      const baseHeight = 1.0;
      const headHeight = 1.0;
      const headThickness = 2.7;
      let remainingHeight = desiredHeight - (baseHeight + headHeight);
      const num2mSections = Math.floor(remainingHeight / 2);
      remainingHeight -= num2mSections * 2;
      const num1mSections = Math.ceil(remainingHeight);

      // Calcula a potência do motor
      let motorPower = (capacity * grainDensity * desiredHeight) / (3600 * beltSpeed * bucketSpacing);
      motorPower = Math.ceil(motorPower);

      // Define a espessura do pé do elevador
      let peEspessura;
      if (desiredHeight <= 10) {
        peEspessura = "1,95 mm";
      } else if (desiredHeight <= 20) {
        peEspessura = "2,75 ou 3,00 mm";
      } else {
        peEspessura = "3,00 ou 4,75 mm";
      }

      // Exibe os resultados
      document.getElementById('result').innerHTML = `
                <div class="card">
                  <i class="fas fa-horse-head"></i> 
                  <p>Potência do Motor: <strong>${motorPower} CV</strong></p>
                </div>
                <div class="card">
                  <i class="fas fa-weight-hanging"></i>
                  <p>Densidade do Grão: <strong>${grainDensity} kg/m³</strong></p>
                </div>
                <div class="card">
                  <i class="fas fa-tachometer-alt"></i>
                  <p>Velocidade da Correia: <strong>${beltSpeed} m/s</strong></p>
                </div>
                <div class="card">
                  <i class="fas fa-arrows-alt-h"></i>
                  <p>Espaçamento entre Canecas: <strong>${bucketSpacing} cm</strong></p>
                </div>
                <div class="card">
                  <i class="fas fa-circle"></i>
                  <p>Diâmetro do Tambor: <strong>${drumDiameter} mm</strong></p>
                </div>
                <div class="card">
                  <i class="fas fa-shoe-prints"></i>
                  <p>Pé do Elevador: <strong>${baseHeight} m</strong> (Espessura: ${peEspessura})</p>
                </div>
                <div class="card">
                  <i class="fas fa-hard-hat"></i>
                  <p>Cabeça do Elevador: <strong>${headHeight} m</strong> (Espessura: ${headThickness} mm)</p>
                </div>
                <div class="card">
                  <i class="fas fa-ruler-combined"></i>
                  <p>Calhas de 2 metros: <strong>${num2mSections}</strong></p>
                </div>
                <div class="card">
                  <i class="fas fa-ruler"></i>
                  <p>Calhas de 1 metro: <strong>${num1mSections}</strong></p>
                </div>
            `;
    }
  </script>
</body>
</html>