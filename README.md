<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SmartPharmacy</title>

<style>
body {
  font-family: 'Segoe UI', sans-serif;
  margin: 0;
  background: #f4f6f9;
}

header {
  background: #2c7be5;
  color: white;
  padding: 15px;
  text-align: center;
  font-size: 22px;
}

.container {
  padding: 20px;
  max-width: 800px;
  margin: auto;
}

.card {
  background: white;
  padding: 20px;
  border-radius: 15px;
  margin-bottom: 20px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}

h2 {
  margin-top: 0;
}

input, select, button {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  border-radius: 10px;
  border: 1px solid #ccc;
}

button {
  background: #2c7be5;
  color: white;
  cursor: pointer;
}

button:hover {
  background: #1a5edb;
}

.result {
  margin-top: 15px;
  font-weight: bold;
}
</style>
</head>

<body>

<header>💊 SmartPharmacy System</header>

<div class="container">

<!-- CEK GEJALA -->
<div class="card">
<h2>Cek Gejala</h2>
<select id="gejala">
  <option value="">Pilih Gejala</option>
  <option value="demam">Demam</option>
  <option value="batuk">Batuk</option>
  <option value="diare">Diare</option>
</select>
<button onclick="cekObat()">Rekomendasi Obat</button>
<div class="result" id="hasilGejala"></div>
</div>

<!-- DATABASE OBAT -->
<div class="card">
<h2>Database Obat</h2>
<select id="obat">
  <option value="">Pilih Obat</option>
  <option value="paracetamol">Paracetamol</option>
  <option value="ibuprofen">Ibuprofen</option>
  <option value="loperamide">Loperamide</option>
</select>
<button onclick="detailObat()">Lihat Detail</button>
<div class="result" id="detail"></div>
</div>

<!-- INTERAKSI OBAT -->
<div class="card">
<h2>Cek Interaksi Obat</h2>
<input type="text" id="obat1" placeholder="Obat 1">
<input type="text" id="obat2" placeholder="Obat 2">
<button onclick="cekInteraksi()">Cek Interaksi</button>
<div class="result" id="interaksi"></div>
</div>

<!-- REMINDER -->
<div class="card">
<h2>Reminder Obat</h2>
<input type="time" id="waktu">
<button onclick="setReminder()">Set Reminder</button>
<div class="result" id="reminder"></div>
</div>

</div>

<script>

// CEK GEJALA
function cekObat() {
  let g = document.getElementById("gejala").value;
  let hasil = "";

  if(g === "demam") hasil = "Paracetamol 500 mg";
  else if(g === "batuk") hasil = "OBH / Dextromethorphan";
  else if(g === "diare") hasil = "Oralit + Loperamide";
  else hasil = "Pilih gejala dulu";

  document.getElementById("hasilGejala").innerText = hasil;
}

// DETAIL OBAT
function detailObat() {
  let o = document.getElementById("obat").value;
  let hasil = "";

  if(o === "paracetamol") {
    hasil = "Dosis: 500 mg | Efek samping: mual | Indikasi: demam";
  }
  else if(o === "ibuprofen") {
    hasil = "Dosis: 200-400 mg | Efek samping: iritasi lambung";
  }
  else if(o === "loperamide") {
    hasil = "Dosis: 2 mg | Indikasi: diare";
  }
  else hasil = "Pilih obat";

  document.getElementById("detail").innerText = hasil;
}

// INTERAKSI
function cekInteraksi() {
  let o1 = document.getElementById("obat1").value.toLowerCase();
  let o2 = document.getElementById("obat2").value.toLowerCase();
  let hasil = "Aman digunakan";

  if((o1 === "ibuprofen" && o2 === "paracetamol")) {
    hasil = "Interaksi ringan, masih bisa digunakan";
  }

  document.getElementById("interaksi").innerText = hasil;
}

// REMINDER
function setReminder() {
  let waktu = document.getElementById("waktu").value;
  document.getElementById("reminder").innerText = "Reminder jam " + waktu;

  setInterval(() => {
    let now = new Date().toTimeString().slice(0,5);
    if(now === waktu) alert("Waktunya minum obat!");
  }, 1000);
}

</script>

</body>
</html>
