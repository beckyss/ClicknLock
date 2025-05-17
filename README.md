<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>ClicknLock - Generator Password Acak</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

    body {
      font-family: 'Poppins', sans-serif;
      background: #001f4d; /* navy */
      color: #f0f0f0;
      margin: 0;
      padding: 3rem 1rem;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center; /* center vertically */
      text-align: center; /* center all text */
    }

    h1 {
      font-weight: 600;
      margin-bottom: 0.5rem;
      text-shadow: 0 0 8px #00000055;
      color: #001f4d;
      background: #f0f0f0;
      border-radius: 10px;
      display: inline-block;
      padding: 0.3em 1em;
    }

    .deskripsi {
      text-align: center;
      max-width: 400px;
      margin: 0 auto 2rem auto;
      font-size: 1rem;
      color: #b3c6e0;
      text-shadow: 0 0 4px #00000044;
      font-style: italic;
    }

    label {
      font-weight: 600;
      margin-bottom: 0.25rem;
      display: block;
      font-size: 0.9rem;
      color: #b3c6e0;
    }

    input[type="number"] {
      width: 80px;
      padding: 0.4rem 0.6rem;
      border-radius: 6px;
      border: none;
      font-size: 1rem;
      text-align: center;
      margin-bottom: 1.5rem;
      outline: none;
      background: #e6ecfa;
      color: #001f4d;
    }

    button {
      background-color: #001f4d;
      color: white;
      border: none;
      padding: 0.75rem 1.75rem;
      font-size: 1.1rem;
      border-radius: 30px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      margin: 0.5rem;
      min-width: 140px;
      box-shadow: 0 6px 15px rgba(0,31,77,0.3);
    }

    button:hover {
      background-color: #003366;
    }

    .kotak-hasil {
      margin-top: 2rem;
      background: rgba(0, 31, 77, 0.15);
      padding: 1.25rem 1.5rem;
      border-radius: 15px;
      font-size: 1.4rem;
      font-family: 'Courier New', Courier, monospace;
      letter-spacing: 0.1em;
      color: #e6ecfa;
      text-align: center;
      min-width: 320px;
      user-select: all;
      box-shadow: 0 0 20px rgba(0,31,77,0.18);
      margin-left: auto;
      margin-right: auto;
    }

    .baris-tombol {
      display: flex;
      gap: 1rem;
      justify-content: center;
      flex-wrap: wrap;
      margin-left: auto;
      margin-right: auto;
    }

    #footer {
      color: #b3c6e0;
      font-size: 1rem;
      margin-top: 3rem;
      text-align: center;
      width: 100%;
      letter-spacing: 0.03em;
      font-weight: 600;
    }
  </style>
</head>
<body>

<h1>ClicknLock</h1>
<div class="deskripsi">Because your security should be simple.</div>

<div>
  <label for="length-input">Panjang Password</label>
  <input type="number" id="length-input" min="6" max="64" value="12" aria-describedby="length-desc" />
  <div id="length-desc" style="font-size:0.75rem; color:#b3c6e0; margin-bottom:1rem;">(Antara 6 dan 64 karakter)</div>
</div>

<div class="baris-tombol">
  <button id="generate-btn" aria-label="Hasilkan password">Hasilkan</button>
  <button id="copy-btn" aria-label="Salin password ke clipboard">Salin</button>
</div>

<div class="kotak-hasil" id="result" aria-live="polite" aria-atomic="true">Password Anda akan muncul di sini</div>

<div id="footer">by kelompok 2 PTI</div>

<script>
(() => {
  const generateBtn = document.getElementById('generate-btn');
  const copyBtn = document.getElementById('copy-btn');
  const resultBox = document.getElementById('result');
  const lengthInput = document.getElementById('length-input');

  const charset = 
    'ABCDEFGHIJKLMNOPQRSTUVWXYZ' +
    'abcdefghijklmnopqrstuvwxyz' +
    '0123456789' +
    '!@#$%^&*()_+-=[]{}|;:,.<>?';

  function generatePassword(length) {
    let password = '';
    for (let i = 0; i < length; i++) {
      const randomIndex = Math.floor(Math.random() * charset.length);
      password += charset[randomIndex];
    }
    return password;
  }

  generateBtn.addEventListener('click', () => {
    let length = parseInt(lengthInput.value, 10);
    if (isNaN(length) || length < 6) length = 6;
    if (length > 64) length = 64;
    const password = generatePassword(length);
    resultBox.textContent = password;
  });

  copyBtn.addEventListener('click', async () => {
    const password = resultBox.textContent;
    if (!password || password === "Password Anda akan muncul di sini") return;
    try {
      await navigator.clipboard.writeText(password);
      copyBtn.textContent = "Tersalin!";
      setTimeout(() => {
        copyBtn.textContent = "Salin";
      }, 1200);
    } catch (e) {
      alert("Gagal menyalin password.");
    }
  });
})();
</script>

</body>
</html>
