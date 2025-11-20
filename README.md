<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>W5o_ Login</title>
<style>
  body, html {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;
    font-family: Arial, sans-serif;
    background: #0a0a0a;
    color: white;
  }
  canvas {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 0;
  }
  .container {
    position: relative;
    z-index: 1;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
  }
  h1 {
    font-size: 50px;
    margin-bottom: 20px;
  }
  input {
    display: block;
    width: 250px;
    padding: 10px;
    margin: 10px 0;
    border-radius: 5px;
    border: none;
    font-size: 16px;
  }
  button {
    padding: 10px 30px;
    margin-top: 10px;
    font-size: 16px;
    border: none;
    border-radius: 5px;
    background: #1e90ff;
    color: white;
    cursor: pointer;
  }
  button:hover {
    background: #1c86ee;
  }
</style>
</head>
<body>

<canvas id="particles"></canvas>

<div class="container">
  <h1>W5o_</h1>
  <input type="email" placeholder="البريد الإلكتروني">
  <input type="password" placeholder="كلمة السر">
  <button>تسجيل دخول</button>
  <button>إنشاء حساب</button>
</div>

<script>
  const canvas = document.getElementById('particles');
  const ctx = canvas.getContext('2d');

  function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }

  window.addEventListener('resize', resizeCanvas);
  resizeCanvas();

  let particleCount = Math.floor((canvas.width * canvas.height) / 6000); // زيادة النقاط حسب حجم الشاشة
  const particles = [];

  class Particle {
    constructor() {
      this.x = Math.random() * canvas.width;
      this.y = Math.random() * canvas.height;
      this.size = 3;
      this.speedX = (Math.random() - 0.5) * 2; 
      this.speedY = (Math.random() - 0.5) * 2;
    }
    update() {
      this.x += this.speedX;
      this.y += this.speedY;
      if(this.x < 0 || this.x > canvas.width) this.speedX *= -1;
      if(this.y < 0 || this.y > canvas.height) this.speedY *= -1;
    }
    draw() {
      ctx.fillStyle = 'rgba(30,144,255,0.8)';
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
      ctx.fill();
    }
  }

  function initParticles() {
    particles.length = 0;
    for(let i = 0; i < particleCount; i++) {
      particles.push(new Particle());
    }
  }

  initParticles();

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    particles.forEach(p => {
      p.update();
      p.draw();
    });
    requestAnimationFrame(animate);
  }

  animate();

  window.addEventListener('resize', () => {
    resizeCanvas();
    particleCount = Math.floor((canvas.width * canvas.height) / 6000);
    initParticles();
  });
</script>

</body>
</html>
