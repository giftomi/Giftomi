<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Video Showcase</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, #1a1a2e, #16213e);
            text-align: center;
            color: #ffffff;
            overflow: hidden;
            position: relative;
        }
        
        .container {
            max-width: 900px;
            background: rgba(255, 255, 255, 0.1);
            padding: 30px;
            border-radius: 12px;
            backdrop-filter: blur(12px);
            box-shadow: 0 4px 20px rgba(255, 255, 255, 0.2);
            animation: fadeIn 1.5s ease-in-out;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        h1 {
            font-size: 36px;
            color: #f1c40f;
            margin-bottom: 10px;
            text-shadow: 0 0 10px rgba(241, 196, 15, 0.8);
            animation: glow 1.5s infinite alternate;
        }

        @keyframes glow {
            from { text-shadow: 0 0 10px rgba(241, 196, 15, 0.8); }
            to { text-shadow: 0 0 20px rgba(241, 196, 15, 1); }
        }
        
        .video-container {
            position: relative;
            width: 100%;
            aspect-ratio: 16 / 9;
            border-radius: 12px;
            overflow: hidden;
            background: transparent;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 15px rgba(255, 255, 255, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            animation: fadeIn 2s ease-in-out;
        }
        
        .video-container:hover {
            transform: scale(2.2);
            box-shadow: 0 4px 25px rgba(255, 255, 255, 0.3);
        }
        
        video {
            width: 100%;
            height: 100%;
            border-radius: 12px;
            opacity: 0.9;
            transition: opacity 0.3s;
        }
        
        video:hover {
            opacity: 1;
        }
        
        .particles {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }
    </style>
</head>
<body>
    <canvas class="particles"></canvas>
    <div class="container">
        <div class="video-container">
            <video controls autoplay loop muted>
                <source src="assets/poto.mp4" type="video/mp4">
                Browser Anda tidak mendukung pemutaran video.
            </video>            
        </div>
    </div>
    
    <script>
        const canvas = document.querySelector('.particles');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        let particlesArray = [];
        
        class Particle {
            constructor(x, y, size, speedX, speedY) {
                this.x = x;
                this.y = y;
                this.size = size;
                this.speedX = speedX;
                this.speedY = speedY;
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                if (this.size > 0.2) this.size -= 0.02;
            }
            draw() {
                ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }
        
        function createParticles() {
            for (let i = 0; i < 100; i++) {
                let size = Math.random() * 3 + 1;
                let x = Math.random() * canvas.width;
                let y = Math.random() * canvas.height;
                let speedX = (Math.random() - 0.5) * 2;
                let speedY = (Math.random() - 0.5) * 2;
                particlesArray.push(new Particle(x, y, size, speedX, speedY));
            }
        }
        
        function animateParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            for (let i = 0; i < particlesArray.length; i++) {
                particlesArray[i].update();
                particlesArray[i].draw();
            }
            requestAnimationFrame(animateParticles);
        }
        
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            particlesArray = [];
            createParticles();
        });
        
        createParticles();
        animateParticles();
    </script>
</body>
</html>

