<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy Birthday, Bestie!</title>
  <style>
    /* Reset & Base */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      min-height: 100vh;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: #ffffff;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow-x: hidden;
      position: relative;
    }

    /* Particles Canvas */
    #particles-canvas {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 1;
      pointer-events: none;
    }

    /* Floating Music Button */
    .music-btn {
      position: fixed;
      top: 20px;
      right: 20px;
      z-index: 10;
      background: rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(8px);
      border: 1px solid rgba(255, 255, 255, 0.3);
      color: #fff;
      width: 45px;
      height: 45px;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      font-size: 1.2rem;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
      transition: transform 0.3s ease, background 0.3s ease;
    }

    .music-btn:hover {
      transform: scale(1.1);
      background: rgba(255, 255, 255, 0.25);
    }

    .music-btn.playing {
      animation: spin 4s linear infinite;
      border-color: #4fc3f7;
    }

    @keyframes spin {
      100% { transform: rotate(360deg); }
    }

    /* Container Card */
    .container {
      position: relative;
      z-index: 2;
      max-width: 800px;
      width: 90%;
      padding: 40px 20px;
      text-align: center;
      background: rgba(255, 255, 255, 0.05);
      backdrop-filter: blur(10px);
      border: 1px solid rgba(255, 255, 255, 0.15);
      border-radius: 20px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
      margin: 20px 0;
    }

    /* Typography */
    h1 {
      font-size: 2.5rem;
      font-weight: 600;
      letter-spacing: 1px;
      margin-bottom: 10px;
      color: #e0f7fa;
      text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
    }

    .subtitle {
      font-size: 1.1rem;
      color: #b2ebf2;
      font-weight: 300;
      margin-bottom: 30px;
    }

    /* Photo Grid */
    .photo-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 15px;
      margin-bottom: 30px;
    }

    .photo-card {
      position: relative;
      border-radius: 12px;
      overflow: hidden;
      aspect-ratio: 1 / 1;
      border: 2px solid rgba(255, 255, 255, 0.2);
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
      transition: transform 0.4s ease, border-color 0.4s ease;
    }

    .photo-card:hover {
      transform: translateY(-5px) scale(1.03);
      border-color: rgba(255, 255, 255, 0.6);
    }

    .photo-card img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }

    /* Message Box */
    .message-box {
      background: rgba(0, 0, 0, 0.2);
      padding: 20px 25px;
      border-radius: 12px;
      border-left: 3px solid #4fc3f7;
    }

    .message-box p {
      font-size: 1rem;
      line-height: 1.6;
      color: #e0f7fa;
      font-weight: 300;
    }

    /* Responsive adjustments */
    @media (max-width: 600px) {
      h1 { font-size: 1.8rem; }
      .photo-grid { grid-template-columns: repeat(2, 1fr); }
    }
  </style>
</head>
<body>

  <!-- Audio Player (Hidden UI, Controlled by Floating Button) -->
  <!-- Ganti 'lagu.mp3' sesuai nama file audio di repositori -->
  <audio id="bg-music" loop>
    <source src="ssstik.io_1785631568856.mp3" type="audio/mpeg">
  </audio>

  <!-- Music Control Button -->
  <div class="music-btn" id="music-toggle" onclick="toggleMusic()">🎵</div>

  <!-- Background Light Particles -->
  <canvas id="particles-canvas"></canvas>

  <!-- Main Content -->
  <div class="container">
    <h1>Selamat Ulang Tahun! ✨</h1>
    <p class="subtitle">Untuk sahabatku</p>

    <!-- 4 Photos Section -->
    <div class="photo-grid">
      <div class="photo-card">
        <img src="e085eaedfd22024b24ca6a1766189716_0.jpeg" alt="Kenangan 1">
      </div>
      <div class="photo-card">
        <img src="bc164bcf9e274738696001f0df26cd06_0.jpeg" alt="Kenangan 2">
      </div>
      <div class="photo-card">
        <img src="IMG-20260710-WA0031.jpg" alt="Kenangan 3">
      </div>
      <div class="photo-card">
        <img src="35e24f89c2d27cfa284b5c34d471b374_0.jpeg" alt="Kenangan 4">
      </div>
    </div>

    <!-- Short Wish Message -->
    <div class="message-box">
      <p>
        Selamat bertambah usia! 
        Semoga di usiamu yang baru ini, segala impianmu perlahan terwujud, selalu diberi kesehatan, 
        serta kebahagiaan yang tak pernah putus. <i>Stay awesome!</i> 🥂✨
      </p>
    </div>
  </div>

  <!-- Scripts -->
  <script>
    /* Audio Control Logic */
    const music = document.getElementById('bg-music');
    const musicBtn = document.getElementById('music-toggle');
    let isPlaying = false;

    function toggleMusic() {
      if (isPlaying) {
        music.pause();
        musicBtn.classList.remove('playing');
        musicBtn.textContent = '🎵';
      } else {
        music.play();
        musicBtn.classList.add('playing');
        musicBtn.textContent = '🎶';
      }
      isPlaying = !isPlaying;
    }

    // Coba putar otomatis saat user pertama kali klik di mana saja pada layar HP
    document.body.addEventListener('click', function() {
      if (!isPlaying) {
        music.play().then(() => {
          isPlaying = true;
          musicBtn.classList.add('playing');
          musicBtn.textContent = '🎶';
        }).catch(() => {
          // Autoplay diblokir browser, pengguna bisa klik tombol musik manual
        });
      }
    }, { once: true });

    /* Floating Particles Script */
    const canvas = document.getElementById('particles-canvas');
    const ctx = canvas.getContext('2d');

    let particles = [];
    const particleCount = 60;

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    class Particle {
      constructor() {
        this.reset();
      }

      reset() {
        this.x = Math.random() * canvas.width;
        this.y = Math.random() * canvas.height;
        this.radius = Math.random() * 2.5 + 0.5;
        this.alpha = Math.random() * 0.6 + 0.2;
        this.speedY = Math.random() * 0.4 + 0.1;
        this.speedX = (Math.random() - 0.5) * 0.2;
      }

      update() {
        this.y -= this.speedY;
        this.x += this.speedX;

        if (this.y < 0 || this.x < 0 || this.x > canvas.width) {
          this.y = canvas.height + 10;
          this.x = Math.random() * canvas.width;
        }
      }

      draw() {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(224, 247, 250, ${this.alpha})`;
        ctx.shadowBlur = 8;
        ctx.shadowColor = '#e0f7fa';
        ctx.fill();
        ctx.closePath();
      }
    }

    function init() {
      particles = [];
      for (let i = 0; i < particleCount; i++) {
        particles.push(new Particle());
      }
    }

    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particles.forEach(p => {
        p.update();
        p.draw();
      });
      requestAnimationFrame(animate);
    }

    init();
    animate();
  </script>

</body>
</html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy Birthday, Bestie!</title>
  <style>
    /* Reset & Base */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      min-height: 100vh;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: #ffffff;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow-x: hidden;
      position: relative;
    }

    /* Particles Canvas */
    #particles-canvas {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 1;
      pointer-events: none;
    }

    /* Container Card */
    .container {
      position: relative;
      z-index: 2;
      max-width: 800px;
      width: 90%;
      padding: 40px 20px;
      text-align: center;
      background: rgba(255, 255, 255, 0.05);
      backdrop-filter: blur(10px);
      border: 1px solid rgba(255, 255, 255, 0.15);
      border-radius: 20px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
      margin: 20px 0;
    }

    /* Typography */
    h1 {
      font-size: 2.5rem;
      font-weight: 600;
      letter-spacing: 1px;
      margin-bottom: 10px;
      color: #e0f7fa;
      text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
    }

    .subtitle {
      font-size: 1.1rem;
      color: #b2ebf2;
      font-weight: 300;
      margin-bottom: 30px;
    }

    /* Photo Grid */
    .photo-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 15px;
      margin-bottom: 30px;
    }

    .photo-card {
      position: relative;
      border-radius: 12px;
      overflow: hidden;
      aspect-ratio: 1 / 1;
      border: 2px solid rgba(255, 255, 255, 0.2);
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
      transition: transform 0.4s ease, border-color 0.4s ease;
    }

    .photo-card:hover {
      transform: translateY(-5px) scale(1.03);
      border-color: rgba(255, 255, 255, 0.6);
    }

    .photo-card img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }

    /* Message Box */
    .message-box {
      background: rgba(0, 0, 0, 0.2);
      padding: 20px 25px;
      border-radius: 12px;
      border-left: 3px solid #4fc3f7;
    }

    .message-box p {
      font-size: 1rem;
      line-height: 1.6;
      color: #e0f7fa;
      font-weight: 300;
    }

    /* Responsive adjustments */
    @media (max-width: 600px) {
      h1 { font-size: 1.8rem; }
      .photo-grid { grid-template-columns: repeat(2, 1fr); }
    }
  </style>
</head>
<body>

  <!-- Background Light Particles -->
  <canvas id="particles-canvas"></canvas>

  <!-- Main Content -->
  <div class="container">
    <h1>Selamat Ulang Tahun! ✨</h1>
    <p class="subtitle">Untuk sahabatku</p>

    <!-- 4 Photos Section -->
    <div class="photo-grid">
      <div class="photo-card">
        <!-- Ganti 'foto1.jpg' dengan nama file fotomu -->
        <img src="e085eaedfd22024b24ca6a1766189716_0.jpeg" alt="Kenangan 1">
      </div>
      <div class="photo-card">
        <!-- Ganti 'foto2.jpg' dengan nama file fotomu -->
        <img src="bc164bcf9e274738696001f0df26cd06_0.jpeg" alt="Kenangan 2">
      </div>
      <div class="photo-card">
        <!-- Ganti 'foto3.jpg' dengan nama file fotomu -->
        <img src="IMG-20260710-WA0031.jpg" alt="Kenangan 3">
      </div>
      <div class="photo-card">
        <!-- Ganti 'foto4.jpg' dengan nama file fotomu -->
        <img src="35e24f89c2d27cfa284b5c34d471b374_0.jpeg" alt="Kenangan 4">
      </div>
    </div>

    <!-- Short Wish Message -->
    <div class="message-box">
      <p>
        Selamat bertambah usia! 
        Semoga di usiamu yang baru ini, segala impianmu perlahan terwujud, selalu diberi kesehatan, 
        serta kebahagiaan yang tak pernah putus. <i>Stay awesome!</i> 🥂✨
      </p>
    </div>
  </div>

  <!-- Floating Particles Script -->
  <script>
    const canvas = document.getElementById('particles-canvas');
    const ctx = canvas.getContext('2d');

    let particles = [];
    const particleCount = 60;

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    class Particle {
      constructor() {
        this.reset();
      }

      reset() {
        this.x = Math.random() * canvas.width;
        this.y = Math.random() * canvas.height;
        this.radius = Math.random() * 2.5 + 0.5;
        this.alpha = Math.random() * 0.6 + 0.2;
        this.speedY = Math.random() * 0.4 + 0.1;
        this.speedX = (Math.random() - 0.5) * 0.2;
      }

      update() {
        this.y -= this.speedY;
        this.x += this.speedX;

        // Reset particle position if it goes off screen
        if (this.y < 0 || this.x < 0 || this.x > canvas.width) {
          this.y = canvas.height + 10;
          this.x = Math.random() * canvas.width;
        }
      }

      draw() {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(224, 247, 250, ${this.alpha})`;
        ctx.shadowBlur = 8;
        ctx.shadowColor = '#e0f7fa';
        ctx.fill();
        ctx.closePath();
      }
    }

    function init() {
      particles = [];
      for (let i = 0; i < particleCount; i++) {
        particles.push(new Particle());
      }
    }

    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particles.forEach(p => {
        p.update();
        p.draw();
      });
      requestAnimationFrame(animate);
    }

    init();
    animate();
  </script>

</body>
</html>
