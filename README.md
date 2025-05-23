<!DOCTYPE html>
<html lang="ms">
<head>
  <meta charset="UTF-8" />
  <title>Kuiz Matematik Sekolah Menengah</title>
  <style>
    body {
      font-family: sans-serif;
      background: #f4f4f4;
      padding: 20px;
      max-width: 700px;
      margin: auto;
    }
    h1, h2 { text-align: center; }
    #container {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px #ccc;
    }
    select, input, button {
      padding: 10px;
      margin-top: 10px;
      width: 100%;
      font-size: 1em;
    }
    #soalan, #result, #skor {
      margin-top: 20px;
      font-weight: bold;
      font-size: 1.1em;
    }
  </style>
</head>
<body>
  <h1>Kuiz Matematik Sekolah Menengah</h1>
  <div id="container">
    <h2>Pilih Tingkatan</h2>
    <select id="tingkatan">
      <option value="1">Tingkatan 1</option>
      <option value="2">Tingkatan 2</option>
      <option value="3">Tingkatan 3</option>
      <option value="4">Tingkatan 4</option>
      <option value="5">Tingkatan 5</option>
    </select>
    <button onclick="mulaKuiz()">Mula Kuiz</button 
    <div id="quiz" style="display:none;">
      <div id="soalan"></div>
      <input type="text" id="jawapan" placeholder="Jawapan anda"/>
      <button onclick="semak()">Hantar</button>
      <div id="result"></div>
      <div id="skor"></div>
    </div>
  </div>

  <script>
    let skor = 0, soalanKe = 0, jawapanBetul = 0, tahap = 1;

    function rawak(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function mulaKuiz() {
      tahap = parseInt(document.getElementById("tingkatan").value);
      document.getElementById("quiz").style.display = "block";
      document.querySelector("select").disabled = true;
      document.querySelector("button").disabled = true;
      skor = 0;
      soalanKe = 0;
      setSoalan();
    }

    function setSoalan() {
      soalanKe++;
      if (soalanKe > 5) {
        document.getElementById("soalan").innerHTML = "Kuiz Tamat!";
        document.getElementById("skor").innerText = `Skor akhir anda: ${skor}/5`;
        document.querySelector("#jawapan").disabled = true;
        return;
      }

      let soalan = "", jawapan = 0;

      switch (tahap) {
        case 1: { // Tingkatan 1: operasi asas
          let a = rawak(10, 50), b = rawak(1, 20);
          soalan = `T1: Hitung ${a} + ${b}`;
          jawapan = a + b;
          break;
        }
        case 2: { // Tingkatan 2: algebra ringkas
          let x = rawak(1, 10), y = rawak(1, 10);
          soalan = `T2: Jika x = ${x}, y = ${y}, hitung 2x + 3y`;
          jawapan = 2 * x + 3 * y;
          break;
        }
        case 3: { // Tingkatan 3: indeks & pecahan
          let a = rawak(2, 5), p = rawak(2, 3);
          soalan = `T3: Hitung ${a}<sup>${p}</sup>`;
          jawapan = a ** p;
          break;
        }
        case 4: { // Tingkatan 4: persamaan linear
          let m = rawak(1, 5), c = rawak(0, 10), x = rawak(1, 10);
          soalan = `T4: Jika y = ${m}x + ${c}, cari y jika x = ${x}`;
          jawapan = m * x + c;
          break;
        }
        case 5: { // Tingkatan 5: fungsi kuadratik mudah
          let a = rawak(1, 3), b = rawak(1, 5), x = rawak(1, 5);
          soalan = `T5: Jika f(x) = ${a}x² + ${b}, cari f(${x})`;
          jawapan = a * x * x + b;
          break;
        }
      }

      jawapanBetul = jawapan;
      document.getElementById("soalan").innerHTML = soalan;
      document.getElementById("jawapan").value = "";
      document.getElementById("result").innerText = "";
    }

    function semak() {
      const input = parseFloat(document.getElementById("jawapan").value);
      if (Math.abs(input - jawapanBetul) < 0.01) {
        skor++;
        document.getElementById("result").innerText = "Betul!";
      } else {
        document.getElementById("result").innerText = `Salah. Jawapan sebenar: ${jawapanBetul}`;
      }
      setTimeout(setSoalan, 1500);
    }
  </script>
</body>
</html>
