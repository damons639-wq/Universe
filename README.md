<!DOCTYPE html>
<style>
    /* 1. RESET DEFAULT BROWSER SPACING - THIS FIXES THE BORDERS */
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body, html {
        width: 100%;
        height: 100%;
        overflow: hidden; /* Prevents scrollbars from appearing */
        background-color: #090a0f; /* Fallback color */
    }

    /* 2. THE BACKGROUND GRADIENT */
    .universe { 
        position: relative; /* Changed to relative to contain children */
        width: 100vw; 
        height: 100vh; 
        background: radial-gradient(circle at center, #1b2735 0%, #090a0f 100%); 
        display: flex;
        align-items: center;
        justify-content: center;
    }

    /* 3. CENTERED CONTENT BOX */
    .content { 
        position: relative; 
        z-index: 10; 
        display: flex; 
        flex-direction: column; 
        align-items: center; 
        text-align: center; 
        pointer-events: none; /* Allows clicks to pass through to the button below */
    }

    /* 4. GLOWING TITLE */
    h1 { 
        font-size: clamp(3rem, 10vw, 5rem); 
        letter-spacing: 12px; 
        text-transform: uppercase; 
        text-shadow: 0 0 20px rgba(95, 237, 131, 0.6); 
        margin: 0; 
        font-weight: 900;
        color: white;
        font-family: sans-serif;
    }

    p { 
        font-size: 1.2rem; 
        color: #888; 
        letter-spacing: 3px; 
        margin-top: 10px;
        margin-bottom: 40px; 
        font-family: sans-serif;
    }

    /* 5. THE NEON BUTTON */
    .btn-get-started {
        pointer-events: auto; /* Re-enables clicks for the button */
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
        font-family: sans-serif;
    }

    .btn-get-started:hover {
        background: #5fed83;
        color: #050505;
        box-shadow: 0 0 40px #5fed83;
        transform: scale(1.05);
        cursor: pointer;
    }

    /* 6. STAR CANVAS POSITIONING */
    #stars { 
        position: absolute; 
        top: 0; 
        left: 0; 
        width: 100%; 
        height: 100%; 
        z-index: 1;
    }
</style>

<div class="universe">
    <canvas id="stars"></canvas>
    
    <div class="content">
        <h1>Universe</h1>
        <p>Exploring the digital void</p>
        <a href="games.html" class="btn-get-started">Get Started</a>
    </div>
</div>

<script>
    const canvas = document.getElementById('stars');
    const ctx = canvas.getContext('2d');
    let stars = [];

    function resize() {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        // Re-init stars on resize to prevent them from "stretching"
        init(); 
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

    window.addEventListener('resize', resize);

    resize(); // Sets initial size and calls init()
    animate();
</script>
