<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VFX MASTER PORTFOLIO</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;600&family=Syncopate:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vanilla-tilt/1.7.2/vanilla-tilt.min.js"></script>

    <style>
        :root {
            --bg-color: #020205;
            --accent-color: #00f3ff;
            --secondary-color: #7000ff;
            --text-color: #ffffff;
            --glass-bg: rgba(255, 255, 255, 0.03);
            --glass-border: rgba(255, 255, 255, 0.08);
        }

        * { box-sizing: border-box; cursor: none; }
        body { margin: 0; background-color: var(--bg-color); color: var(--text-color); font-family: 'Space Grotesk', sans-serif; overflow-x: hidden; }

        #vfx-canvas { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; background: #020205; }

        /* === 1. NAVIGATION BAR === */
        nav {
            position: fixed; top: 0; width: 100%; padding: 25px 5%;
            display: flex; justify-content: space-between; align-items: center;
            z-index: 1000; backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--glass-border);
        }
        .nav-logo { font-family: 'Syncopate', sans-serif; font-weight: 700; font-size: 1.2rem; color: var(--accent-color); }
        .nav-links { display: flex; gap: 25px; }
        .nav-links a { 
            color: white; text-decoration: none; font-size: 0.9rem; 
            letter-spacing: 2px; transition: 0.3s; opacity: 0.7;
        }
        .nav-links a:hover { opacity: 1; color: var(--accent-color); text-shadow: 0 0 10px var(--accent-color); }

        /* === 2. CUSTOM CURSOR === */
        .cursor-dot, .cursor-circle { position: fixed; top: 0; left: 0; transform: translate(-50%, -50%); border-radius: 50%; z-index: 9999; pointer-events: none; }
        .cursor-dot { width: 6px; height: 6px; background: var(--accent-color); box-shadow: 0 0 10px var(--accent-color); }
        .cursor-circle { width: 35px; height: 35px; border: 1px solid rgba(0, 243, 255, 0.3); transition: width 0.3s, height 0.3s, background 0.3s; }
        body.hovering .cursor-circle { width: 60px; height: 60px; background: rgba(0, 243, 255, 0.1); border-color: var(--accent-color); }

        /* === 3. HERO & GRID === */
        header { height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center; }
        .hero-title { font-family: 'Syncopate', sans-serif; font-size: 6vw; text-shadow: 3px 3px var(--secondary-color); }
        
        .container { max-width: 1400px; margin: 0 auto; padding: 100px 5%; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); gap: 40px; }

        .card { 
            background: var(--glass-bg); border: 1px solid var(--glass-border); 
            border-radius: 15px; overflow: hidden; backdrop-filter: blur(10px);
        }

        .card-thumbnail { width: 100%; height: 230px; background-size: cover; position: relative; }
        .play-button { 
            position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);
            width: 50px; height: 50px; border: 1px solid var(--accent-color); border-radius: 50%;
            display: flex; justify-content: center; align-items: center; background: rgba(0,0,0,0.5);
        }

        /* === 4. CONTACT & SOCIALS SECTION === */
        .contact-section {
            padding: 100px 5%; text-align: center;
            background: linear-gradient(to bottom, transparent, rgba(112, 0, 255, 0.05));
        }
        .social-icons { display: flex; justify-content: center; gap: 40px; margin: 40px 0; }
        .social-icons a { font-size: 2rem; color: white; transition: 0.4s; }
        .social-icons a:hover { color: var(--accent-color); transform: translateY(-10px); }

        .contact-btn {
            padding: 15px 40px; border: 1px solid var(--accent-color);
            background: transparent; color: white; font-family: 'Syncopate';
            font-size: 0.8rem; letter-spacing: 3px; transition: 0.3s;
        }
        .contact-btn:hover { background: var(--accent-color); color: black; box-shadow: 0 0 30px var(--accent-color); }

        /* === LIGHTBOX === */
        .lightbox { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.95); z-index: 5000; display: none; justify-content: center; align-items: center; }
        .lightbox.active { display: flex; }
        .video-wrapper { width: 80%; aspect-ratio: 16/9; }

        footer { padding: 50px; text-align: center; color: #444; font-size: 0.7rem; letter-spacing: 2px; }

        @media(max-width: 768px) {
            .nav-links { display: none; }
            .hero-title { font-size: 3rem; }
        }
    </style>
</head>
<body>

    <canvas id="vfx-canvas"></canvas>
    <div class="cursor-dot"></div>
    <div class="cursor-circle"></div>

    <nav>
        <div class="nav-logo">VFX.CORE</div>
        <div class="nav-links">
            <a href="#work">PORTFOLIO</a>
            <a href="https://your-shop-link.com" target="_blank"><i class="fas fa-shopping-cart"></i> SHOP</a>
            <a href="#contact">CONTACT</a>
        </div>
    </nav>

    <header>
        <div class="hero-title">YOUR NAME</div>
        <p style="letter-spacing: 8px; color: #888;">VISUAL EFFECTS & MOTION</p>
    </header>

    <div class="container" id="work">
        <div class="grid">
            <div class="card" data-tilt onclick="openVideo('https://www.youtube.com/embed/dQw4w9WgXcQ')">
                <div class="card-thumbnail" style="background-image: url('https://images.unsplash.com/photo-1535016120720-40c6874c3b13?auto=format&fit=crop&w=800&q=80');">
                    <div class="play-button"><i class="fas fa-play"></i></div>
                </div>
                <div class="card-info" style="padding: 20px;">
                    <h3>PROJECT ALPHA</h3>
                    <div style="font-size: 0.7rem; color: var(--accent-color); margin-top: 10px;">[ VIEW REEL ]</div>
                </div>
            </div>
            </div>
    </div>

    <section class="contact-section" id="contact">
        <h2 style="font-family: 'Syncopate';">GET IN TOUCH</h2>
        
        <div class="social-icons">
            <a href="https://youtube.com/@yourchannel" target="_blank"><i class="fab fa-youtube"></i></a>
            <a href="https://instagram.com/yourprofile" target="_blank"><i class="fab fa-instagram"></i></a>
            <a href="https://t.me/yourchannel" target="_blank"><i class="fab fa-telegram"></i></a>
            <a href="mailto:your@email.com"><i class="fas fa-envelope"></i></a>
        </div>

        <button class="contact-btn" onclick="location.href='mailto:your@email.com'">START A PROJECT</button>
    </section>

    <div class="lightbox" id="videoModal" onclick="closeVideo()">
        <div class="video-wrapper">
            <iframe id="videoFrame" src="" allow="autoplay; encrypted-media" allowfullscreen></iframe>
        </div>
    </div>

    <footer>&copy; 2026 YOUR NAME | BUILT FOR THE FUTURE</footer>

    <script>
        // === VFX PLEXUS BACKGROUND ===
        const canvas = document.getElementById('vfx-canvas');
        const ctx = canvas.getContext('2d');
        let particles = [];

        function init() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            particles = [];
            for (let i = 0; i < 80; i++) {
                particles.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height,
                    vx: (Math.random() - 0.5) * 0.5,
                    vy: (Math.random() - 0.5) * 0.5
                });
            }
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach((p, i) => {
                p.x += p.vx; p.y += p.vy;
                if (p.x < 0 || p.x > canvas.width) p.vx *= -1;
                if (p.y < 0 || p.y > canvas.height) p.vy *= -1;

                ctx.fillStyle = 'rgba(0, 243, 255, 0.5)';
                ctx.beginPath();
                ctx.arc(p.x, p.y, 1.5, 0, Math.PI * 2);
                ctx.fill();

                for (let j = i + 1; j < particles.length; j++) {
                    const p2 = particles[j];
                    const dist = Math.hypot(p.x - p2.x, p.y - p2.y);
                    if (dist < 150) {
                        ctx.strokeStyle = `rgba(0, 243, 255, ${1 - dist / 150})`;
                        ctx.lineWidth = 0.5;
                        ctx.beginPath();
                        ctx.moveTo(p.x, p.y);
                        ctx.lineTo(p2.x, p2.y);
                        ctx.stroke();
                    }
                }
            });
            requestAnimationFrame(animate);
        }

        window.addEventListener('resize', init);
        init(); animate();

        // === CURSOR & MODAL LOGIC ===
        const dot = document.querySelector('.cursor-dot');
        const circle = document.querySelector('.cursor-circle');
        window.addEventListener('mousemove', e => {
            dot.style.left = circle.style.left = `${e.clientX}px`;
            dot.style.top = circle.style.top = `${e.clientY}px`;
        });

        document.querySelectorAll('a, button, .card').forEach(el => {
            el.addEventListener('mouseenter', () => document.body.classList.add('hovering'));
            el.addEventListener('mouseleave', () => document.body.classList.remove('hovering'));
        });

        function openVideo(url) {
            document.getElementById('videoModal').classList.add('active');
            document.getElementById('videoFrame').src = url;
        }
        function closeVideo() {
            document.getElementById('videoModal').classList.remove('active');
            document.getElementById('videoFrame').src = "";
        }
    </script>
</body>
</html>
