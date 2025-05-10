<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Centralny Rejestr Elektryków</title>
  <link rel="icon" href="favicon.png" type="image/png" />
  <link rel="manifest" href="manifest.json" />

  <style>
    * {
      margin: 5px;
      padding: 0;
      box-sizing: border-box;
    }

    html, body {
      height: 100%;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to bottom right, #f0f0f0, #dcdcdc);
      color: #000;
      display: flex;
      flex-direction: column;
    }

     .container {
      display: flex;
      align-items: center;
      gap: 20px;
    }
      .logo {
      width: 100px;
    }

    .text {
      font-size: 36px;
      line-height: 1.2;
    }

    .text span {
      display: block;
    }

    .black {
      color: #000;
    }

    .blue {
      color: #003d7c;
    }

    header {
      display: flex;
      align-items: center;
      padding: 10px 20px;
      background: transparent;
    }

    header img {
      height: 200px;
      max-width: none;
      margin-top: -15px;
    }

    .section-text {
      text-align: justify;
      max-width: 300px;
      margin: 0 auto;
      padding: 10px;
    }

    .content {
      flex: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding-top: 10px;
      padding-bottom: 40px;
    }

    .grid {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 40px;
      padding: 0 20px;
      text-align: center;
    }

    .box {
      background-color: #e6e6e6;
      padding: 40px 20px;
      width: 250px;
      border: 1px solid #ccc;
      border-radius: 10px;
      transition: tra nsform 0.2s ease;
    }

    .box:hover {
      transform: scale(1.05);
    }

    .box img {
      width: 55px;
      margin-bottom: 20px;
    }

    .box p {
      font-size: 1em;
      color: #003366;
    }

    .features {
      display: flex;
      justify-content: center;
      gap: 60px;
      margin-top: 50px;
      flex-wrap: wrap;
      text-align: center;
      padding: 0 20px;
    }

    .feature {
      max-width: 240px;
    }

    .feature img {
      width: 60px;
      margin-bottom: 15px;
    }

    .feature h3 {
      margin-bottom: 10px;
      color: #003366;
      font-size: 1.1em;
    }

    a.box {
      text-decoration: none;
      color: inherit;
      display: block;
    }

    .feature p {
      font-size: 0.95em;
      color: #444;
      text-align: justify;
      max-width: 300px;
      margin: 0 auto;
      padding: 10px;
    }

    footer {
      background-color: #222;
      color: #ccc;
      text-align: center;
      padding: 10px 20px;
      font-size: 0.9em;
    }

    footer a {
      color: #00bbff;
      text-decoration: none;
      margin: 0 10px;
    }

    footer a:hover {
      text-decoration: underline;
    }

    @media (max-width: 768px) {
      header {
        justify-content: center;
      }

      .grid {
        flex-direction: column;
        align-items: center;
      }

      .features {
        flex-direction: column;
        align-items: center;
      }
    }

    /* styl logowania */
    .login-button {
      position: absolute;
      top: 20px;
      right: 20px;
      cursor: pointer;
    }

    .login-button svg {
      width: 24px;
      height: 24px;
      fill: #000;
    }

    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.5);
      justify-content: center;
      align-items: center;
    }

    .modal-content {
      background-color: #fff;
      padding: 30px;
      border-radius: 8px;
      text-align: center;
      width: 300px;
    }

    .modal-content button {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      font-size: 16px;
      cursor: pointer;
    }

    .google-button {
      background-color: #4285F4;
      color: white;
      border: none;
    }

    .facebook-button {
      background-color: #3B5998;
      color: white;
      border: none;
    }
  </style>
</head>
<body>

  <!-- Górna część strony z logo -->
  <header>
    <img src="logo.png" alt="Logo Centralny Rejestr Elektryków" />
    <p>Centralny Rejestr Elektryków</p>
  </header>

  <!-- logowanie elementy, przyciski itd -->
  <div class="login-button" onclick="openModal()" id="loginIcon">
    <!-- Ikona ludzika -->
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
      <path d="M12 12c2.7 0 4.8-2.1 4.8-4.8S14.7 2.4 12 2.4 7.2 4.5 7.2 7.2 9.3 12 12 12zm0 2.4c-3.2 0-9.6 1.6-9.6 4.8V22h19.2v-2.8c0-3.2-6.4-4.8-9.6-4.8z"/>
    </svg>
  </div>

  <div class="modal" id="loginModal">
    <div class="modal-content">
      <h2>Zaloguj się</h2>
      <button class="google-button" onclick="login('google')">Kontynuuj z Google</button>
      <button class="facebook-button" onclick="login('facebook')">Kontynuuj z Facebook</button>
    </div>
  </div>

  <script>
    function openModal() {
      document.getElementById('loginModal').style.display = 'flex';
    }

    window.onclick = function(event) {
      const modal = document.getElementById('loginModal');
      if (event.target === modal) {
        modal.style.display = "none";
      }
    }

    function login(provider) {
      const iconDiv = document.getElementById("loginIcon");
      iconDiv.innerHTML = `
        <!-- Ikona z "check" -->
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
          <path fill="green" d="M9 16.2l-4.2-4.2L3.4 13.4l5.6 5.6 12-12L19.2 5l-10.2 11.2z"/>
        </svg>
      `;
      document.getElementById('loginModal').style.display = 'none';
    }
  </script>

  <!-- Środkowa część z kafelkami -->
  <div class="content">
    <main class="grid">
      <a href="rejestracja.html" class="box">
        <img src="orzel_1.png" alt="Orzeł 1" />
        <p>JESTEM ELEKTRYKIEM REJESTRACJA</p>
      </a>
      <a href="wyszukiwarka.html" class="box">
        <img src="orzel_2.png" alt="Orzeł 2" />
        <p>SZUKAM ELEKTRYKA</p>
      </a>
      <a href="profil.html" class="box">
        <img src="orzel_3.png" alt="Orzeł 3" />
        <p>PROFIL ELEKTRYKA</p>
      </a>
    </main>

    <section class="features">
      <div class="feature">
        <img src="bezpieczenstwo.png" alt="Bezpieczeństwo" />
        <h3>Bezpieczeństwo</h3>
        <p>Weryfikacja uprawnień i certyfikatów w czasie rzeczywistym...</p>
      </div>
      <div class="feature">
        <img src="certyfikowani.png" alt="Certyfikowani fachowcy" />
        <h3>Certyfikowani fachowcy</h3>
        <p>Wyłącznie certyfikowani i sprawdzeni fachowcy...</p>
      </div>
      <div class="feature">
        <img src="rejestracja.png" alt="Rejestracja" />
        <h3>Rejestracja</h3>
        <p>Prosta rejestracja i szybki dostęp do danych</p>
      </div>
    </section>
  </div>

  <!-- Stopka -->
  <footer>
    &copy; 2025 Centralny Rejestr Elektryków<br />
    <a href="#">Regulamin</a> |
    <a href="#">Polityka prywatności</a> |
    <a href="#">Kontakt</a>
  </footer>

</body>
</html>

