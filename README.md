<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dinkaira Elsa - UI/UX Designer & Frontend Developer</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.min.js"></script>
    <style>
        :root {
            --primary: #6366F1;
            --primary-dark: #4F46E5;
            --dark: #0F172A;
            --light: #F8FAFC;
            --gray: #64748B;
            --gray-light: #E2E8F0;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: var(--dark);
            color: var(--light);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        /* Header Section */
        .header {
            text-align: center;
            padding: 60px 0 40px;
            background: linear-gradient(135deg, #0F172A 0%, #1E293B 100%);
            position: relative;
            overflow: hidden;
        }
        
        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: radial-gradient(circle at 30% 20%, rgba(99, 102, 241, 0.1) 0%, transparent 50%);
            z-index: 0;
        }
        
        .profile-img {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            border: 4px solid var(--primary);
            margin: 0 auto 20px;
            background: linear-gradient(45deg, #4F46E5, #7C3AED);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 48px;
            color: white;
            position: relative;
            z-index: 1;
        }
        
        .name {
            font-size: 2.5rem;
            margin-bottom: 10px;
            background: linear-gradient(to right, #8B5CF6, #6366F1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            position: relative;
            z-index: 1;
        }
        
        .tagline {
            font-size: 1.2rem;
            color: var(--gray-light);
            margin-bottom: 20px;
            position: relative;
            z-index: 1;
        }
        
        .typing-container {
            height: 60px;
            margin: 20px 0;
            position: relative;
            z-index: 1;
        }
        
        .typing-text {
            font-size: 1.5rem;
            font-weight: 600;
            color: var(--primary);
            display: inline-block;
            border-right: 3px solid var(--primary);
            white-space: nowrap;
            overflow: hidden;
            animation: typing 3.5s steps(40, end), blink-caret 0.75s step-end infinite;
        }
        
        @keyframes typing {
            from { width: 0 }
            to { width: 100% }
        }
        
        @keyframes blink-caret {
            from, to { border-color: transparent }
            50% { border-color: var(--primary) }
        }
        
        /* About Section */
        .section {
            padding: 60px 0;
        }
        
        .section-title {
            text-align: center;
            font-size: 2rem;
            margin-bottom: 40px;
            position: relative;
        }
        
        .section-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background: var(--primary);
            border-radius: 2px;
        }
        
        .about-content {
            display: flex;
            flex-wrap: wrap;
            gap: 40px;
            align-items: center;
        }
        
        .about-text {
            flex: 1;
            min-width: 300px;
        }
        
        .about-text p {
            margin-bottom: 20px;
            color: var(--gray-light);
        }
        
        .focus-list {
            list-style: none;
            margin-top: 20px;
        }
        
        .focus-list li {
            margin-bottom: 10px;
            display: flex;
            align-items: center;
        }
        
        .focus-list li::before {
            content: '▹';
            color: var(--primary);
            margin-right: 10px;
        }
        
        /* 3D Model Section */
        .model-container {
            flex: 1;
            min-width: 300px;
            height: 400px;
            position: relative;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            background: linear-gradient(145deg, #1E293B, #0F172A);
        }
        
        #model-canvas {
            width: 100%;
            height: 100%;
            display: block;
        }
        
        /* Tools Section */
        .tools-section {
            background: linear-gradient(135deg, #1E293B 0%, #0F172A 100%);
            padding: 60px 0;
        }
        
        .tools-category {
            margin-bottom: 40px;
        }
        
        .category-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: var(--primary);
            display: flex;
            align-items: center;
        }
        
        .category-title::before {
            content: '';
            display: inline-block;
            width: 10px;
            height: 10px;
            background: var(--primary);
            border-radius: 50%;
            margin-right: 10px;
        }
        
        .tools-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 15px;
        }
        
        .tool-item {
            background: rgba(30, 41, 59, 0.7);
            border-radius: 8px;
            padding: 15px 10px;
            text-align: center;
            transition: all 0.3s ease;
            border: 1px solid rgba(99, 102, 241, 0.1);
        }
        
        .tool-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(99, 102, 241, 0.2);
            border-color: var(--primary);
        }
        
        .tool-icon {
            font-size: 2rem;
            margin-bottom: 10px;
            color: var(--primary);
        }
        
        .tool-name {
            font-size: 0.9rem;
            color: var(--gray-light);
        }
        
        /* Stats Section */
        .stats-section {
            padding: 60px 0;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }
        
        .stat-card {
            background: linear-gradient(135deg, #1E293B 0%, #334155 100%);
            border-radius: 12px;
            padding: 30px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
        }
        
        .stat-card:hover {
            transform: translateY(-5px);
        }
        
        .stat-number {
            font-size: 2.5rem;
            font-weight: bold;
            color: var(--primary);
            margin-bottom: 10px;
        }
        
        .stat-label {
            color: var(--gray-light);
            font-size: 1rem;
        }
        
        /* Contact Section */
        .contact-section {
            background: linear-gradient(135deg, #1E293B 0%, #0F172A 100%);
            padding: 60px 0;
            text-align: center;
        }
        
        .social-links {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 30px;
        }
        
        .social-link {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: rgba(99, 102, 241, 0.1);
            color: var(--primary);
            font-size: 1.2rem;
            transition: all 0.3s ease;
            text-decoration: none;
        }
        
        .social-link:hover {
            background: var(--primary);
            color: white;
            transform: translateY(-3px);
        }
        
        /* Footer */
        .footer {
            text-align: center;
            padding: 30px 0;
            background: #0A0F1C;
            color: var(--gray);
            font-size: 0.9rem;
        }
        
        .quote {
            font-style: italic;
            margin-top: 20px;
            color: var(--gray-light);
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            .name {
                font-size: 2rem;
            }
            
            .typing-text {
                font-size: 1.2rem;
            }
            
            .tools-grid {
                grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
            }
            
            .model-container {
                height: 300px;
            }
        }
    </style>
</head>
<body>
    <!-- Header Section -->
    <header class="header">
        <div class="container">
            <div class="profile-img">DE</div>
            <h1 class="name">Dinkaira Elsa</h1>
            <p class="tagline">UI/UX Designer | Frontend Developer | Creative Problem Solver</p>
            <div class="typing-container">
                <div class="typing-text">Building Amazing Digital Experiences</div>
            </div>
        </div>
    </header>

    <!-- About Section -->
    <section class="section">
        <div class="container">
            <h2 class="section-title">About Me</h2>
            <div class="about-content">
                <div class="about-text">
                    <p>Hi! I'm <strong>Dinkaira Elsa</strong>, a passionate <strong>UI/UX Designer & Frontend Developer</strong> with a keen eye for creating seamless, intuitive digital experiences and building scalable frontend architectures.</p>
                    
                    <p><strong>Current Focus:</strong></p>
                    <ul class="focus-list">
                        <li>Building intuitive user interfaces</li>
                        <li>Creating seamless user experiences</li>
                        <li>Frontend development with modern frameworks</li>
                        <li>Design systems and component libraries</li>
                    </ul>
                    
                    <p><strong>Life Philosophy:</strong><br>
                    <em>"Design is not just what it looks like – design is how it works."</em></p>
                </div>
                
                <!-- 3D Model Container -->
                <div class="model-container">
                    <canvas id="model-canvas"></canvas>
                </div>
            </div>
        </div>
    </section>

    <!-- Tools Section -->
    <section class="tools-section">
        <div class="container">
            <h2 class="section-title">Skills & Technologies</h2>
            
            <div class="tools-category">
                <h3 class="category-title">Design & Creativity</h3>
                <div class="tools-grid">
                    <div class="tool-item">
                        <div class="tool-icon">🎨</div>
                        <div class="tool-name">Figma</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">✏️</div>
                        <div class="tool-name">Illustrator</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">🖼️</div>
                        <div class="tool-name">Photoshop</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">🚀</div>
                        <div class="tool-name">Framer</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">🎬</div>
                        <div class="tool-name">After Effects</div>
                    </div>
                </div>
            </div>
            
            <div class="tools-category">
                <h3 class="category-title">Frontend Development</h3>
                <div class="tools-grid">
                    <div class="tool-item">
                        <div class="tool-icon">⚛️</div>
                        <div class="tool-name">React</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">🅰️</div>
                        <div class="tool-name">Angular</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">📦</div>
                        <div class="tool-name">Vue.js</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">📱</div>
                        <div class="tool-name">React Native</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">🔄</div>
                        <div class="tool-name">Redux</div>
                    </div>
                </div>
            </div>
            
            <div class="tools-category">
                <h3 class="category-title">Styling & UI Frameworks</h3>
                <div class="tools-grid">
                    <div class="tool-item">
                        <div class="tool-icon">🎐</div>
                        <div class="tool-name">Tailwind</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">🅱️</div>
                        <div class="tool-name">Bootstrap</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">🎨</div>
                        <div class="tool-name">CSS3</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">📄</div>
                        <div class="tool-name">HTML5</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">💎</div>
                        <div class="tool-name">SASS</div>
                    </div>
                </div>
            </div>
            
            <div class="tools-category">
                <h3 class="category-title">Programming Languages</h3>
                <div class="tools-grid">
                    <div class="tool-item">
                        <div class="tool-icon">🟨</div>
                        <div class="tool-name">JavaScript</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">🔷</div>
                        <div class="tool-name">TypeScript</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">🐍</div>
                        <div class="tool-name">Python</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">☕</div>
                        <div class="tool-name">Java</div>
                    </div>
                    <div class="tool-item">
                        <div class="tool-icon">➕</div>
                        <div class="tool-name">C++</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Stats Section -->
    <section class="stats-section">
        <div class="container">
            <h2 class="section-title">GitHub Statistics</h2>
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-number">50+</div>
                    <div class="stat-label">Projects Completed</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">25+</div>
                    <div class="stat-label">Happy Clients</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">3+</div>
                    <div class="stat-label">Years Experience</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">15+</div>
                    <div class="stat-label">Technologies</div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section class="contact-section">
        <div class="container">
            <h2 class="section-title">Connect With Me</h2>
            <p>Let's collaborate and create something amazing together!</p>
            
            <div class="social-links">
                <a href="https://twitter.com/dink_sira" class="social-link" target="_blank">
                    🐦
                </a>
                <a href="https://www.linkedin.com/in/dinksira-elsa-13904b319/" class="social-link" target="_blank">
                    💼
                </a>
                <a href="https://instagram.com/dink.sira" class="social-link" target="_blank">
                    📸
                </a>
                <a href="https://www.behance.net/dinksira%20elsa%20samuel" class="social-link" target="_blank">
                    🎨
                </a>
                <a href="https://www.upwork.com/freelancers/~0169e7871bfcb02264?mp_source=share" class="social-link" target="_blank">
                    💻
                </a>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
        <div class="container">
            <p>&copy; 2023 Dinkaira Elsa. All rights reserved.</p>
            <p class="quote">"Design is not just what it looks like and feels like. Design is how it works." - Steve Jobs</p>
        </div>
    </footer>

    <script>
        // 3D Model Setup
        let scene, camera, renderer, controls;
        let computer;
        
        function init() {
            // Create scene
            scene = new THREE.Scene();
            scene.background = new THREE.Color(0x0F172A);
            
            // Create camera
            camera = new THREE.PerspectiveCamera(75, 1, 0.1, 1000);
            camera.position.z = 5;
            
            // Create renderer
            const canvas = document.getElementById('model-canvas');
            renderer = new THREE.WebGLRenderer({ canvas, antialias: true });
            renderer.setSize(canvas.clientWidth, canvas.clientHeight);
            renderer.setPixelRatio(window.devicePixelRatio);
            
            // Add lights
            const ambientLight = new THREE.AmbientLight(0x6366F1, 0.5);
            scene.add(ambientLight);
            
            const directionalLight = new THREE.DirectionalLight(0xffffff, 0.8);
            directionalLight.position.set(5, 5, 5);
            scene.add(directionalLight);
            
            const pointLight = new THREE.PointLight(0x6366F1, 0.5);
            pointLight.position.set(-5, -5, 5);
            scene.add(pointLight);
            
            // Create computer model
            createComputer();
            
            // Add orbit controls
            controls = new THREE.OrbitControls(camera, renderer.domElement);
            controls.enableDamping = true;
            controls.dampingFactor = 0.05;
            
            // Handle window resize
            window.addEventListener('resize', onWindowResize);
            
            // Start animation
            animate();
        }
        
        function createComputer() {
            const group = new THREE.Group();
            
            // Monitor
            const monitorGeometry = new THREE.BoxGeometry(3, 2, 0.2);
            const monitorMaterial = new THREE.MeshPhongMaterial({ 
                color: 0x1E293B,
                shininess: 30
            });
            const monitor = new THREE.Mesh(monitorGeometry, monitorMaterial);
            monitor.position.y = 1;
            group.add(monitor);
            
            // Screen
            const screenGeometry = new THREE.PlaneGeometry(2.8, 1.8);
            const screenMaterial = new THREE.MeshBasicMaterial({ 
                color: 0x6366F1,
                emissive: 0x6366F1,
                emissiveIntensity: 0.3
            });
            const screen = new THREE.Mesh(screenGeometry, screenMaterial);
            screen.position.set(0, 1, 0.11);
            group.add(screen);
            
            // Stand
            const standGeometry = new THREE.CylinderGeometry(0.1, 0.3, 1, 8);
            const standMaterial = new THREE.MeshPhongMaterial({ 
                color: 0x334155,
                shininess: 50
            });
            const stand = new THREE.Mesh(standGeometry, standMaterial);
            stand.position.y = -0.5;
            group.add(stand);
            
            // Base
            const baseGeometry = new THREE.CylinderGeometry(0.8, 0.8, 0.2, 16);
            const baseMaterial = new THREE.MeshPhongMaterial({ 
                color: 0x1E293B,
                shininess: 30
            });
            const base = new THREE.Mesh(baseGeometry, baseMaterial);
            base.position.y = -1.1;
            group.add(base);
            
            // Keyboard
            const keyboardGeometry = new THREE.BoxGeometry(2.5, 0.1, 1);
            const keyboardMaterial = new THREE.MeshPhongMaterial({ 
                color: 0x0F172A,
                shininess: 20
            });
            const keyboard = new THREE.Mesh(keyboardGeometry, keyboardMaterial);
            keyboard.position.set(0, -1.2, 1.2);
            group.add(keyboard);
            
            scene.add(group);
            computer = group;
        }
        
        function onWindowResize() {
            const container = document.querySelector('.model-container');
            camera.aspect = container.clientWidth / container.clientHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(container.clientWidth, container.clientHeight);
        }
        
        function animate() {
            requestAnimationFrame(animate);
            
            if (computer) {
                computer.rotation.y += 0.005;
            }
            
            controls.update();
            renderer.render(scene, camera);
        }
        
        // Initialize when page loads
        window.addEventListener('load', init);
    </script>
</body>
</html>
