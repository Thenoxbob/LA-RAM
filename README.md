<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>LA RAM – Landing Page</title>

  <!-- CSS -->
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', sans-serif;
    }

    body {
      background: radial-gradient(circle at top, #0f2027, #000);
      color: #fff;
      overflow-x: hidden;
    }

    header {
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      position: relative;
    }

    header::before {
      content: "";
      position: absolute;
      inset: 0;
      background: url('https://images.unsplash.com/photo-1518770660439-4636190af475') center/cover;
      opacity: 0.15;
    }

    .hero {
      position: relative;
      z-index: 2;
      max-width: 900px;
      padding: 20px;
      animation: fadeIn 1.5s ease forwards;
    }

    .hero h1 {
      font-size: clamp(2.5rem, 6vw, 4.5rem);
      letter-spacing: 4px;
      margin-bottom: 20px;
      text-transform: uppercase;
    }

    .hero p {
      font-size: 1.2rem;
      opacity: 0.85;
      margin-bottom: 40px;
    }

    .btn {
      padding: 15px 40px;
      border-radius: 50px;
      border: 2px solid #00f2ff;
      background: transparent;
      color: #00f2ff;
      font-size: 1rem;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    .btn:hover {
      background: #00f2ff;
      color: #000;
      transform: scale(1.05);
    }

    section {
      padding: 100px 10%;
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 30px;
    }

    .card {
      background: rgba(255,255,255,0.05);
      border-radius: 20px;
      padding: 30px;
      backdrop-filter: blur(10px);
      transform: translateY(40px);
      opacity: 0;
      transition: 0.6s ease;
    }

    .card.show {
      transform: translateY(0);
      opacity: 1;
    }

    .card h3 {
      margin-bottom: 15px;
      color: #00f2ff;
    }

    footer {
      text-align: center;
      padding: 40px;
      font-size: 0.9rem;
      opacity: 0.6;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Particules */
    canvas {
      position: fixed;
      inset: 0;
      z-index: 0;
    }
  </style>
</head>
<body>

  <canvas id="particles"></canvas>

  <header>
    <div class="hero">
      <h1>LA RAM</h1>
      <p>La mémoire vive nouvelle génération. Rapide. Fluide. Intelligente.</p>
      <button class="btn">Découvrir</button>
    </div>
  </header>

  <section>
    <div class="cards">
      <div class="card">
        <h3>Ultra Rapide</h3>
        <p>Des performances optimisées pour les applications modernes.</p>
      </div>
      <div class="card">
        <h3>Stabilité</h3>
        <p>Une gestion intelligente des données pour une fiabilité maximale.</p>
      </div>
      <div class="card">
        <h3>Technologie Future</h3>
        <p>Conçue pour l’IA, le gaming et le cloud computing.</p>
      </div>
    </div>
  </section>

  <footer>
    © 2025 LA RAM – Tous droits réservés
  </footer>

  <!-- JavaScript -->
  <script>
    /* Animation scroll cards */
    const cards = document.querySelectorAll('.card');

    const observer = new IntersectionObserver(entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('show');
        }
      });
    }, { threshold: 0.2 });

    cards.forEach(card => observer.observe(card));

    /* Particules */
    const canvas = document.getElementById('particles');
    const ctx = canvas.getContext('2d');
    let particles = [];

    function resize() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resize);
    resize();

    class Particle {
      constructor() {
        this.x = Math.random() * canvas.width;
        this.y = Math.random() * canvas.height;
        this.vx = (Math.random() - 0.5) * 0.6;
        this.vy = (Math.random() - 0.5) * 0.6;
        this.size = Math.random() * 2 + 1;
      }
      draw() {
        ctx.fillStyle = 'rgba(0,242,255,0.7)';
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
        ctx.fill();
      }
      update() {
        this.x += this.vx;
        this.y += this.vy;
        if (this.x < 0 || this.x > canvas.width) this.vx *= -1;
        if (this.y < 0 || this.y > canvas.height) this.vy *= -1;
        this.draw();
      }
    }

    function initParticles() {
      particles = [];
      for (let i = 0; i < 100; i++) {
        particles.push(new Particle());
      }
    }

    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particles.forEach(p => p.update());
      requestAnimationFrame(animate);
    }

    initParticles();
    animate();
  </script>
</body>
</html>
