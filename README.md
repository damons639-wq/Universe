<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Universe Portfolio</title>
    <style>
        /* 1. THE SPACE THEME COLORS */
        body, html { 
            margin: 0; 
            padding: 0; 
            width: 100%; 
            height: 100%; 
            overflow: hidden; 
            background: #050505; 
            color: white; 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
        }

        /* 2. THE BACKGROUND GRADIENT */
        .universe { 
            position: absolute; 
            width: 100%; 
            height: 100%; 
            background: radial-gradient(circle at center, #1b2735 0%, #090a0f 100%); 
        }

        /* 3. CENTERED CONTENT BOX */
        .content { 
            position: relative; 
            z-index: 10; 
            display: flex; 
            flex-direction: column; 
            align-items: center; 
            justify-content: center; 
            height: 100vh; 
            text-align: center; 
        }

        /* 4. GLOWING TITLE */
        h1 { 
            font-size: clamp(3rem, 10vw, 5rem); 
            letter-spacing: 12px; 
            text-transform: uppercase; 
            text-shadow: 0 0 20px #5fed83; 
            margin: 0; 
            font-weight: 900;
        }

        p { 
            font-size: 1.2rem; 
            color: #888; 
            letter-spacing: 3px; 
            margin-bottom: 40px; 
        }

        /* 5. THE NEON BUTTON */
        .btn-get-started {
            padding: 18px 45px;
            font-size: 1.1rem;
            font-weight: bold;
            color: #5fed83;
            text-decoration: none;
            letter-spacing: 4px;
            border: 2px solid #5fed83;
            border-radius: 50px;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 0 15px rgba(95, 237, 131, 0.2);
            text-transform: uppercase;
        }

        .btn-get-started:hover {
            background: #5fed83;
            color: #050505;
            box-shadow: 0 0 40px #5fed83;
            transform: scale(1.1);
            cursor: pointer;
        }

        /* 6. STAR CANVAS POSITIONING */
        #stars { 
            position: absolute; 
            top: 0; 
            left: 0; 
            width: 100%; 
            height: 100%; 
        }
    </style>
</head>
<body>
    <div class="universe">
        <!-- Canvas for the animated star background -->
        <canvas id="stars"></canvas>
        
        <!-- Main visible text and button -->
        <div class="content">
            <h1>Universe</h1>
            <p>Exploring the digital void</p>
            <a href="games.html" class="btn-get-started">Get Started</a>
        </div>
    </div>

    <script>
        /* 7. STAR ANIMATION SCRIPT */
        const canvas = document.getElementById('stars');
        const ctx = canvas.getContext('2d');
        let stars = [];

        function resize() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }

        class Star {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2;
                this.speed = Math.random() * 0.4 + 0.1;
            }
            draw() {
                ctx.fillStyle = "rgba(255, 255, 255, 0.8)";
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
            update() {
                this.y += this.speed;
                if (this.y > canvas.height) {
                    this.y = 0;
                    this.x = Math.random() * canvas.width;
                }
            }
        }

        function init() {
            resize();
            stars = [];
            for (let i = 0; i < 250; i++) {
                stars.push(new Star());
            }
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            stars.forEach(s => {
                s.update();
                s.draw();
            });
            requestAnimationFrame(animate);
        }

        window.addEventListener('resize', () => {
            init();
        });

        init();
        animate();
    </script>
</body>
</html>
