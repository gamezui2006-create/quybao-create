<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tối nay khó ngủ quá...</title>
  <style>
    body {
      margin: 0;
      height: 100vh;
      background: linear-gradient(135deg, #1e0033, #330033, #660066);
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-family: "Poppins", sans-serif;
      overflow: hidden;
    }

    h1 {
      font-size: 2em;
      text-align: center;
      animation: fadeIn 2s ease-in-out;
    }

    .btn-container {
      margin-top: 20px;
      display: flex;
      gap: 20px;
    }

    button {
      font-size: 1.2em;
      padding: 10px 25px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    #yesBtn {
      background: #ff4da6;
      color: white;
      box-shadow: 0 0 10px #ff4da6;
    }

    #noBtn {
      background: #444;
      color: #fff;
      position: absolute;
    }

    #message {
      margin-top: 30px;
      font-size: 1.8em;
      color: #ffb6c1;
      animation: fadeIn 1.5s ease-in-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Hiệu ứng tim bay */
    .heart {
      position: fixed;
      bottom: 0;
      font-size: 24px;
      animation: floatUp 5s linear infinite;
      opacity: 0.8;
    }

    @keyframes floatUp {
      from {
        transform: translateY(0) scale(1);
        opacity: 1;
      }
      to {
        transform: translateY(-100vh) scale(1.5);
        opacity: 0;
      }
    }
  </style>
</head>
<body>

  <h1>Tối nay khó ngủ quá...<br>Có muốn biết lý do không? 💭</h1>

  <div class="btn-container">
    <button id="yesBtn">Có 💖</button>
    <button id="noBtn">Không 😝</button>
  </div>

  <div id="message"></div>

  <!-- Nhạc nền -->
  <audio id="bgMusic" autoplay loop hidden>
    <source src="https://cdn.pixabay.com/download/audio/2023/03/16/audio_3b6c9941e8.mp3?filename=romantic-piano-ambient-142199.mp3" type="audio/mp3">
  </audio>

  <script>
    const yesBtn = document.getElementById('yesBtn');
    const noBtn = document.getElementById('noBtn');
    const message = document.getElementById('message');

    // Khi nhấn "Có"
    yesBtn.addEventListener('click', () => {
      message.innerHTML = "Vì anh nhớ em đó 🥺❤️";
      createHearts();
    });

    // Khi rê chuột vào "Không" thì nó né đi
    noBtn.addEventListener('mouseover', () => {
      const x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
      const y = Math.random() * (window.innerHeight - noBtn.offsetHeight);
      noBtn.style.left = `${x}px`;
      noBtn.style.top = `${y}px`;
    });

    // Hiệu ứng tim bay
    function createHearts() {
      setInterval(() => {
        const heart = document.createElement("div");
        heart.classList.add("heart");
        heart.innerHTML = "💖";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.animationDuration = (3 + Math.random() * 2) + "s";
        document.body.appendChild(heart);
        setTimeout(() => heart.remove(), 5000);
      }, 300);
    }
  </script>

</body>
</html>
