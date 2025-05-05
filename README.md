<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Cadastro de Folga Funcionários</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-color: #121212;
      --card-color: #1e1e1e;
      --text-color: #ffffff;
      --input-bg: #2c2c2c;
      --border-color: #444;
      --highlight-color: #673ab7;
    }

    * {
      box-sizing: border-box;
    }

    body {
      font-family: 'Inter', sans-serif;
      background-color: var(--bg-color);
      color: var(--text-color);
      margin: 0;
      padding: 40px 20px;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
    }

    .form-container {
      background: var(--card-color);
      padding: 40px;
      border-radius: 12px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
      width: 100%;
      max-width: 1000px;
      display: flex;
      flex-direction: column;
      gap: 20px;
    }

    .form-container h2 {
      text-align: center;
      margin-top: 0;
    }

    .form-header {
      text-align: center;
      margin-bottom: 10px;
    }

    .form-header img {
      width: 60px;
      margin-bottom: 10px;
    }

    fieldset {
      border: none;
      padding: 0;
    }

    .form-group legend {
      font-size: 15px;
      font-weight: 600;
      margin-bottom: 8px;
      color: var(--text-color);
    }

    label {
      display: block;
      margin-bottom: 8px;
      font-size: 14px;
    }

    input[type="radio"],
    input[type="date"],
    input[type="text"],
    select {
      font-size: 14px;
      padding: 10px;
      border-radius: 6px;
      border: 1px solid var(--border-color);
      background-color: var(--input-bg);
      color: var(--text-color);
      width: 100%;
      margin-bottom: 10px;
    }

    option {
      background: var(--input-bg);
      color: var(--text-color);
    }

    .radio-group label {
      display: inline-block;
      margin-right: 15px;
    }

    #motivoOutros {
      display: none;
    }

    button {
      background: var(--highlight-color);
      color: white;
      border: none;
      padding: 14px;
      border-radius: 6px;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      width: 100%;
      transition: background 0.3s;
    }

    button:hover {
      background: #5e35b1;
    }

    @media (max-width: 600px) {
      .radio-group label {
        display: block;
        margin-right: 0;
      }
    }
  </style>
</head>
<body>
  <div class="form-container">
    <div class="form-header">
      <img src="https://cdn-icons-png.flaticon.com/512/747/747310.png" alt="Calendário">
      <h2>CADASTRO DE FOLGA FUNCIONÁRIOS</h2>
    </div>
    <form id="form" method="POST" action="https://script.google.com/macros/s/AKfycbwh-YUwL2o3_i-bfcV9RMzLcoI98vyyGwEXf4LHlG5KJ59gIAlUe1_VVlFQMBqU6PwR/exec">
      <fieldset class="form-group" id="filialGroup">
        <legend>Filial</legend>
        <div class="radio-group">
          <label><input type="radio" name="filial" value="ARTUR"> ARTUR</label>
          <label><input type="radio" name="filial" value="FLORIANO"> FLORIANO</label>
          <label><input type="radio" name="filial" value="JOTA"> JOTA</label>
          <label><input type="radio" name="filial" value="MODA"> MODA</label>
          <label><input type="radio" name="filial" value="PONTO"> PONTO</label>
        </div>
      </fieldset>

      <fieldset class="form-group" id="funcionarioGroup">
        <legend>Funcionário</legend>
        <select id="funcionario" name="funcionario">
          <option value="">Selecione a filial primeiro</option>
        </select>
      </fieldset>

      <fieldset class="form-group">
        <legend>DIA TRABALHADO</legend>
        <input type="date" id="dataTrabalho" name="dataTrabalho">
      </fieldset>

      <fieldset class="form-group" id="motivoGroup">
        <legend>Motivo da Folga</legend>
        <div class="radio-group">
          <label><input type="radio" name="motivo" value="DOMINGO"> DOMINGO</label>
          <label><input type="radio" name="motivo" value="FERIADO"> FERIADO</label>
          <label><input type="radio" name="motivo" value="OUTROS"> OUTROS</label>
        </div>
      </fieldset>

      <fieldset class="form-group" id="motivoOutros">
        <legend>Especificar o Motivo</legend>
        <input type="text" name="outrosMotivo" placeholder="Escreva o motivo">
      </fieldset>

      <fieldset class="form-group">
        <legend>Data da Folga</legend>
        <input type="date" id="dataFolga" name="dataFolga">
      </fieldset>

      <button type="submit">Enviar</button>
    </form>
  </div>

  <script>
    const funcionariosPorFilial = {
      "ARTUR": ["FERNANDA", "LUCILENE"],
      "FLORIANO": ["FERNANDA", "MEIRE", "SARA", "THACIANNE"],
      "JOTA": ["BRUNO", "CARINA", "DENISE", "FABIOLA", "JÉSSICA", "LOUISE", "NATALIA", "PRISCILA", "RAYSSA", "VERA"],
      "MODA": ["ANA CLARA", "DAIANE", "JÉSSICA", "MARCIA", "NAISE", "GLENDA", "MARIA"],
      "PONTO": ["DANIELA", "DEBORA", "ISADORA", "PAULA", "PRISCILA", "SANDY", "SÔNIA", "SUELI"]
    };

    document.getElementById('filialGroup').addEventListener('change', function() {
      const filialSelecionada = document.querySelector('input[name="filial"]:checked');
      const funcionarioSelect = document.getElementById('funcionario');
      funcionarioSelect.innerHTML = "<option value=''>Selecione um funcionário</option>";

      if (filialSelecionada) {
        funcionariosPorFilial[filialSelecionada.value].forEach(function(funcionario) {
          const option = document.createElement("option");
          option.value = funcionario;
          option.textContent = funcionario;
          funcionarioSelect.appendChild(option);
        });
      }
    });

    document.querySelectorAll('input[name="motivo"]').forEach(function(radio) {
      radio.addEventListener('change', function () {
        const dataTrabalhoInput = document.getElementById("dataTrabalho");
        const dataFolgaInput = document.getElementById("dataFolga");
        const motivoOutrosField = document.getElementById("motivoOutros");

        if (!dataTrabalhoInput.value) {
          alert("Selecione primeiro a Data de Trabalho!");
          this.checked = false;
          return;
        }

        const dataTrabalho = new Date(dataTrabalhoInput.value);
        const maxDate = new Date(dataTrabalho);

        if (this.value === "DOMINGO") {
          maxDate.setDate(dataTrabalho.getDate() + 7);
        } else if (this.value === "FERIADO" || this.value === "OUTROS") {
          maxDate.setDate(dataTrabalho.getDate() + 60);
        }

        dataFolgaInput.min = dataTrabalho.toISOString().split('T')[0];
        dataFolgaInput.max = maxDate.toISOString().split('T')[0];

        motivoOutrosField.style.display = this.value === "OUTROS" ? "block" : "none";
      });
    });

    document.getElementById("form").addEventListener("submit", function (event) {
      event.preventDefault();
      const formData = new FormData(this);

      fetch(this.action, {
        method: "POST",
        body: formData
      })
        .then(response => response.text())
        .then(data => {
          alert("Folga cadastrada com sucesso!");
          this.reset();
          document.getElementById("funcionario").innerHTML = '<option value="">Selecione a filial primeiro</option>';
          document.getElementById("motivoOutros").style.display = "none";
        })
        .catch(error => alert("Erro ao enviar os dados!"));
    });
  </script>
</body>
</html>
