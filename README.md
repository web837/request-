
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Request Video Mobil - New Creativity</title>
  <style>
    body, html {
      margin: 0; padding: 0; height: 100%;
      font-family: Arial, sans-serif;
      background: url('https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=1350&q=80') no-repeat center center fixed;
      background-size: cover;
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
    }
    .container {
      background: rgba(0, 0, 0, 0.7);
      padding: 30px;
      border-radius: 12px;
      max-width: 400px;
      width: 90%;
      box-sizing: border-box;
      box-shadow: 0 0 10px rgba(0,0,0,0.8);
      margin-top: 40px;
    }
    h1 {
      text-align: center;
      margin-bottom: 20px;
      font-weight: 700;
    }
    label {
      display: block;
      margin: 15px 0 5px 0;
      font-weight: 600;
    }
    input[type="text"] {
      width: 100%;
      padding: 10px;
      font-size: 1rem;
      border-radius: 6px;
      border: none;
      box-sizing: border-box;
    }
    button {
      margin-top: 20px;
      padding: 12px;
      width: 100%;
      border: none;
      border-radius: 25px;
      font-weight: 700;
      font-size: 1rem;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    button:disabled {
      background-color: #777;
      cursor: not-allowed;
      color: #ccc;
    }
    #subscribeBtn {
      background-color: #cc0000;
      color: white;
    }
    #subscribeBtn:disabled {
      background-color: #555;
    }
    #sendBtn.enabled {
      background-color: #00c853;
      color: white;
    }
    #sendBtn.disabled {
      background-color: #777;
      color: #ccc;
      cursor: not-allowed;
    }
    footer {
      margin-top: 20px;
      font-style: italic;
      text-align: center;
      user-select: none;
    }
    /* Language selector styles */
    .lang-selector {
      position: fixed;
      top: 10px;
      right: 20px;
      background: rgba(0,0,0,0.6);
      border-radius: 25px;
      overflow: hidden;
      display: flex;
      box-shadow: 0 0 6px rgba(0,0,0,0.7);
      user-select: none;
    }
    .lang-button {
      padding: 8px 18px;
      cursor: pointer;
      color: white;
      background: transparent;
      border: none;
      font-weight: 700;
      font-size: 0.9rem;
      transition: background 0.3s ease;
    }
    .lang-button.active {
      background: #00c853;
      color: #fff;
    }
    .lang-button:not(.active):hover {
      background: rgba(255,255,255,0.1);
    }
  </style>
</head>
<body>

  <!-- Language selector -->
  <div class="lang-selector">
    <button id="lang-id" class="lang-button active">Indonesia</button>
    <button id="lang-en" class="lang-button">English</button>
  </div>

  <div class="container">
    <h1 id="title">Apa yang ingin kamu request?</h1>

    <label for="nameInput" id="label-name">Nama Pemesan</label>
    <input type="text" id="nameInput" placeholder="Ketik nama Anda" autocomplete="off" />

    <label for="carInput" id="label-car">Jenis Mobil</label>
    <input type="text" id="carInput" placeholder="Ketik jenis mobil" autocomplete="off" />

    <label for="editInput" id="label-edit">Jenis Edit</label>
    <input type="text" id="editInput" placeholder="Ketik jenis edit yang diinginkan" autocomplete="off" />

    <button id="subscribeBtn">Subscribe Channel YouTube</button>
    <button id="sendBtn" class="disabled" disabled>Kirim</button>
  </div>

  <footer id="footer">by new creativity</footer>

  <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>
  <script type="text/javascript">
    (function(){
      emailjs.init({
        publicKey: "YOUR_PUBLIC_KEY" // Ganti dengan publicKey EmailJS Anda
      });
    })();
  </script>

  <script>
    const translations = {
      id: {
        title: "Apa yang ingin kamu request?",
        labelName: "Nama Pemesan",
        namePlaceholder: "Ketik nama Anda",
        labelCar: "Jenis Mobil",
        carPlaceholder: "Ketik jenis mobil",
        labelEdit: "Jenis Edit",
        editPlaceholder: "Ketik jenis edit yang diinginkan",
        subscribeBtn: "Subscribe Channel YouTube",
        sendBtn: "Kirim",
        sendingBtn: "Mengirim...",
        subscribedBtn: "Subscribed!",
        footer: "by new creativity",
        alertFill: "Mohon isi semua kolom terlebih dahulu.",
        alertSuccess: "Request Anda berhasil dikirim. Terima kasih sudah subscribe dan mengirim request!",
        alertFail: "Gagal mengirim: "
      },
      en: {
        title: "What do you want to request?",
        labelName: "Requester Name",
        namePlaceholder: "Type your name",
        labelCar: "Car Type",
        carPlaceholder: "Type the car type",
        labelEdit: "Edit Type",
        editPlaceholder: "Type the desired edit",
        subscribeBtn: "Subscribe to YouTube Channel",
        sendBtn: "Send",
        sendingBtn: "Sending...",
        subscribedBtn: "Subscribed!",
        footer: "by new creativity",
        alertFill: "Please fill in all fields first.",
        alertSuccess: "Your request has been sent. Thank you for subscribing and sending the request!",
        alertFail: "Failed to send: "
      }
    };

    // Elements
    const langIdBtn = document.getElementById('lang-id');
    const langEnBtn = document.getElementById('lang-en');
    const title = document.getElementById('title');
    const labelName = document.getElementById('label-name');
    const nameInput = document.getElementById('nameInput');
    const labelCar = document.getElementById('label-car');
    const carInput = document.getElementById('carInput');
    const labelEdit = document.getElementById('label-edit');
    const editInput = document.getElementById('editInput');
    const subscribeBtn = document.getElementById('subscribeBtn');
    const sendBtn = document.getElementById('sendBtn');
    const footer = document.getElementById('footer');

    let currentLang = 'id';

    function setLanguage(lang) {
      currentLang = lang;
      const t = translations[lang];

      title.textContent = t.title;
      labelName.textContent = t.labelName;
      nameInput.placeholder = t.namePlaceholder;
      labelCar.textContent = t.labelCar;
      carInput.placeholder = t.carPlaceholder;
      labelEdit.textContent = t.labelEdit;
      editInput.placeholder = t.editPlaceholder;
      subscribeBtn.textContent = t.subscribeBtn;
      sendBtn.textContent = t.sendBtn;
      footer.textContent = t.footer;

      langIdBtn.classList.toggle('active', lang==='id');
      langEnBtn.classList.toggle('active', lang==='en');
    }

    langIdBtn.addEventListener('click', () => setLanguage('id'));
    langEnBtn.addEventListener('click', () => setLanguage('en'));

    setLanguage(currentLang);

    // EmailJS initialization
    (function(){
      emailjs.init({
        publicKey: "Q5lQIJmB1pkdeat79" // Ganti dengan publicKey EmailJS Anda
      });
    })();

    // Helper to check inputs filled
    function inputsNotEmpty() {
      return nameInput.value.trim() !== '' &&
             carInput.value.trim() !== '' &&
             editInput.value.trim() !== '';
    }

    sendBtn.disabled = true;
    sendBtn.classList.add('disabled');

    subscribeBtn.addEventListener('click', () => {
      window.open("https://www.youtube.com/channel/UCRx9x0B52oPDvgtsGfP2SWA", '_blank');
      subscribeBtn.disabled = true;
      subscribeBtn.textContent = translations[currentLang].subscribedBtn;
      subscribeBtn.style.backgroundColor = '#4caf50';

      if (inputsNotEmpty()) {
        sendBtn.disabled = false;
        sendBtn.classList.remove('disabled');
        sendBtn.classList.add('enabled');
        sendBtn.textContent = translations[currentLang].sendBtn;
      }
    });

    function checkEnableSendBtn() {
      if (subscribeBtn.disabled && inputsNotEmpty()) {
        sendBtn.disabled = false;
        sendBtn.classList.remove('disabled');
        sendBtn.classList.add('enabled');
        sendBtn.textContent = translations[currentLang].sendBtn;
      } else {
        sendBtn.disabled = true;
        sendBtn.classList.remove('enabled');
        sendBtn.classList.add('disabled');
        sendBtn.textContent = translations[currentLang].sendBtn;
      }
    }

    nameInput.addEventListener('input', checkEnableSendBtn);
    carInput.addEventListener('input', checkEnableSendBtn);
    editInput.addEventListener('input', checkEnableSendBtn);

    sendBtn.addEventListener('click', () => {
      if (!inputsNotEmpty()) {
        alert(translations[currentLang].alertFill);
        return;
      }
      sendBtn.disabled = true;
      sendBtn.textContent = translations[currentLang].sendingBtn;

      emailjs.send('newanda', 'template_request', {
        name: nameInput.value.trim(),
        car: carInput.value.trim(),
        edit: editInput.value.trim()
      }).then(() => {
        alert(translations[currentLang].alertSuccess);
        nameInput.value = '';
        carInput.value = '';
        editInput.value = '';
        sendBtn.textContent = translations[currentLang].sendBtn;
        sendBtn.disabled = true;
        sendBtn.classList.remove('enabled');
        sendBtn.classList.add('disabled');
        subscribeBtn.disabled = false;
        subscribeBtn.textContent = translations[currentLang].subscribeBtn;
        subscribeBtn.style.backgroundColor = '#cc0000';
      }).catch(error => {
        alert(translations[currentLang].alertFail + JSON.stringify(error));
        sendBtn.textContent = translations[currentLang].sendBtn;
        sendBtn.disabled = false;
      });
    });
  </script>

</body>
</html>
