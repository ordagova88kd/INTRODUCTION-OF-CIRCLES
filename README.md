<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Geometry Explorer - Digital Learning</title>
    
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.css">
    <script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.js"></script>
    <script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/contrib/auto-render.min.js" 
        onload="renderMathInElement(document.body, {delimiters: [{left: '\\(', right: '\\)', display: false}]});"></script>

    <style>
        /* CSS Reset & Global Styles */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: #273142; 
            color: #333;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* --- LOGIN SCREEN --- */
        #login-screen {
            background-color: #ffffff;
            width: 100%;
            max-width: 450px;
            margin-top: 80px;
            border-radius: 12px;
            padding: 40px 30px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            position: relative;
        }
        #login-screen::before {
            content: '';
            position: absolute;
            top: 40px;
            left: 30px;
            width: 4px;
            height: 32px;
            background-color: #e74c3c;
        }
        .login-header {
            text-align: center;
            margin-bottom: 30px;
        }
        .login-title {
            font-size: 28px;
            font-weight: 900;
            margin-bottom: 10px;
            text-transform: uppercase;
            padding-left: 10px;
            display: flex;
            justify-content: center;
            gap: 8px;
        }
        .text-dark { color: #1a1a1a; }
        .text-red { color: #e74c3c; }
        .login-subtitle {
            color: #7f8c8d;
            font-size: 14px;
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #4b5563;
            font-size: 14px;
        }
        .form-control {
            width: 100%;
            padding: 12px;
            border: 1px solid #d1d5db;
            border-radius: 6px;
            font-size: 15px;
            transition: border-color 0.2s;
        }
        .form-control:focus {
            outline: none;
            border-color: #3498db;
        }
        .btn-submit {
            width: 100%;
            padding: 14px;
            background-color: #e74c3c;
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 10px;
            transition: background-color 0.2s;
        }
        .btn-submit:hover { background-color: #c0392b; }

        /* --- MAIN APP SCREEN --- */
        #main-app {
            display: none;
            width: 100%;
            max-width: 1000px;
            margin-top: 20px;
            margin-bottom: 40px;
        }
        
        .top-bar {
            background-color: #1e2633;
            border-radius: 8px;
            padding: 12px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: #a0b2c6;
            font-size: 14px;
            margin-bottom: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        .top-bar-left { display: flex; align-items: center; gap: 15px; }
        .top-bar-right { display: flex; align-items: center; gap: 10px; }
        .user-info { font-weight: 600; color: #ffffff; }

        .app-container {
            background-color: #ffffff;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
        }

        .tabs-header {
            display: flex;
            background-color: #f8f9fa;
            border-bottom: 2px solid #e9ecef;
        }
        .tab-btn {
            flex: 1;
            padding: 16px 5px;
            background: none;
            border: none;
            border-bottom: 3px solid transparent;
            font-size: 14px;
            font-weight: 700;
            color: #6c757d;
            cursor: pointer;
            transition: all 0.2s;
            text-transform: uppercase;
        }
        .tab-btn:hover { color: #3498db; }
        .tab-btn.active {
            color: #3498db;
            border-bottom-color: #3498db;
            background-color: #ffffff;
        }

        .tab-content {
            display: none;
            padding: 30px;
            animation: fadeIn 0.3s ease-in-out;
        }
        .tab-content.active { display: block; }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .section-title {
            color: #2c3e50;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 22px;
        }
        .section-title::before {
            content: '';
            display: block;
            width: 4px;
            height: 24px;
            background-color: #e74c3c;
        }

        .instruction {
            color: #7f8c8d;
            margin-bottom: 20px;
            font-size: 15px;
            background-color: #f8f9fa;
            padding: 10px 15px;
            border-radius: 6px;
            border-left: 3px solid #3498db;
        }

        .control-panel {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: #f8f9fa;
            padding: 15px 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            border: 1px solid #e9ecef;
        }
        .slider-group { display: flex; align-items: center; gap: 15px; }
        
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            font-weight: bold;
            color: white;
            transition: opacity 0.2s;
        }
        .btn:hover { opacity: 0.9; }
        .btn-danger { background-color: #e74c3c; }
        .btn-primary { background-color: #6c5ce7; }

        .canvas-container {
            text-align: center;
            position: relative;
        }
        canvas {
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            background-color: #fdfdfd;
            cursor: crosshair;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.02);
            max-width: 100%;
        }

        .info-text { font-size: 18px; font-weight: bold; color: #2c3e50; }
        .result-box {
            margin-top: 20px; padding: 15px; border-radius: 6px;
            font-size: 18px; font-weight: bold; text-align: center;
        }
        .result-trong { background-color: #fff3cd; color: #856404; border: 1px solid #ffeeba; }
        .result-tren { background-color: #d4edda; color: #155724; border: 1px solid #c3e6cb; }
        .result-ngoai { background-color: #f8d7da; color: #721c24; border: 1px solid #f5c6cb; }
        .result-default { background-color: #e2e3e5; color: #383d41; border: 1px solid #d6d8db; }

        .distance-display {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.9);
            padding: 10px 15px;
            border-radius: 6px;
            border: 1px solid #3498db;
            font-family: monospace;
            font-size: 16px;
            font-weight: bold;
            color: #2c3e50;
            pointer-events: none;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            text-align: left;
        }
    </style>
</head>
<body>

    <div id="login-screen">
        <div class="login-header">
            <div style="font-size: 40px; margin-bottom: -10px;">📐</div>
            <br>
            <div class="login-title">
                <span class="text-dark">MATH</span>
                <span class="text-red">EXPLORER</span>
            </div>
            <div class="login-subtitle">Enter your information to access the learning system.</div>
        </div>

        <div class="form-group">
            <label for="hoTen">Full Name</label>
            <input type="text" id="hoTen" class="form-control" placeholder="e.g., Dao Vinh Khang">
        </div>
        <div class="form-group">
            <label for="tenLop">Class</label>
            <select id="tenLop" class="form-control">
                <option value="">-- Select your class --</option>
                <option value="9A">Class 9A</option>
                <option value="9B">Class 9B</option>
                <option value="9C">Class 9C</option>
                <option value="9D">Class 9D</option>
                <option value="9E">Class 9E</option>
                <option value="9F">Class 9F</option>
                <option value="9G">Class 9G</option>
                <option value="9H">Class 9H</option>
                <option value="9I">Class 9I</option>
            </select>
        </div>
        <button class="btn-submit" onclick="dangNhap()">ACCESS SYSTEM</button>
    </div>

    <div id="main-app">
        <div class="top-bar">
            <div class="top-bar-left">
                <span>👨‍🎓 Role: Student</span>
                <span>|</span>
                <span>Name: <span id="display-name" class="user-info">...</span></span>
                <span>|</span>
                <span>Class: <span id="display-class" class="user-info">...</span></span>
            </div>
            <div class="top-bar-right">
                <span>⏱ Session time: <span id="session-time">00:00</span></span>
            </div>
        </div>

        <div class="app-container">
            <div class="tabs-header">
                <button class="tab-btn active" onclick="openTab(event, 'Tab1')">PART 1: LOCUS</button>
                <button class="tab-btn" onclick="openTab(event, 'Tab2')">PART 2: INTERSECTION</button>
                <button class="tab-btn" onclick="openTab(event, 'Tab3')">PART 3: LINE SYMMETRY</button>
                <button class="tab-btn" onclick="openTab(event, 'Tab4')">PART 4: POINT SYMMETRY</button>
            </div>

            <div id="Tab1" class="tab-content active">
                <h3 class="section-title">Exploring the Locus of a Point</h3>
                <div class="instruction">
                    ℹ️ Instruction: Press and hold point P, then move it around center O to observe its path (locus).
                </div>
                <div class="control-panel">
                    <div class="slider-group">
                        <label for="radiusSlider1"><b>Radius R: </b><span id="rValue1">100</span></label>
                        <input type="range" id="radiusSlider1" min="50" max="200" value="100" oninput="updateTab1()">
                    </div>
                    <button class="btn btn-danger" onclick="clearTrail1()">Clear Locus</button>
                </div>
                <div class="canvas-container">
                    <canvas id="canvasTab1" width="800" height="400"></canvas>
                </div>
            </div>

            <div id="Tab2" class="tab-content">
                <h3 class="section-title">Relative Position of a Point and a Circle</h3>
                <div class="instruction">
                    ℹ️ Instruction: Drag point M to any position (inside, on, or outside) to observe its relationship with circle (O, R).
                </div>
                <div class="control-panel">
                    <div class="slider-group">
                        <label for="radiusSlider2"><b>Radius R: </b><span id="rValue2">120</span></label>
                        <input type="range" id="radiusSlider2" min="50" max="200" value="120" oninput="updateTab2()">
                    </div>
                    <div class="info-text">Distance OM = <span id="omValue" style="color:#e74c3c;">...</span></div>
                </div>
                <div class="canvas-container">
                    <canvas id="canvasTab2" width="800" height="400"></canvas>
                </div>
                <div id="ketLuanBox" class="result-box result-default">
                    Move point M to see the conclusion
                </div>
            </div>

            <div id="Tab3" class="tab-content">
                <h3 class="section-title">Line Symmetry in Nature</h3>
                <div class="instruction">
                    ℹ️ Instruction: Use your mouse to <b>trace the edge of half the leaf</b>. Observe the symmetric point on the other side and its distance to the axis of symmetry.
                </div>
                <div class="control-panel">
                    <span>The dashed line in the middle is the <b>Axis of symmetry \(\Delta\)</b></span>
                    <button class="btn btn-primary" onclick="clearTrail3()">ERASE</button>
                </div>
                <div class="canvas-container">
                    <div id="distanceDisplay" class="distance-display">
                        d(A, Δ) = 0<br>d(A', Δ) = 0
                    </div>
                    <canvas id="canvasTab3" width="800" height="450"></canvas>
                </div>
            </div>

            <div id="Tab4" class="tab-content">
                <h3 class="section-title">Point Symmetry in Geometry</h3>
                <div class="instruction">
                    ℹ️ Instruction: Use your mouse to <b>trace the pinwheel pattern</b> or draw freely. Observe how point A' reflects through the center of symmetry O.
                </div>
                <div class="control-panel">
                    <span>The red dot in the center is the <b>Center of symmetry \(O\)</b></span>
                    <button class="btn btn-primary" onclick="clearTrail4()">ERASE</button>
                </div>
                <div class="canvas-container">
                    <div id="distanceDisplay4" class="distance-display">
                        d(A, O) = 0<br>d(A', O) = 0
                    </div>
                    <canvas id="canvasTab4" width="800" height="450"></canvas>
                </div>
            </div>

        </div>
    </div>

<script>
    // --- TIMER & LOGIN LOGIC ---
    let timerInterval;
    let seconds = 0;

    function startTimer() {
        timerInterval = setInterval(() => {
            seconds++;
            let m = Math.floor(seconds / 60).toString().padStart(2, '0');
            let s = (seconds % 60).toString().padStart(2, '0');
            document.getElementById('session-time').innerText = `${m}:${s}`;
        }, 1000);
    }

    function dangNhap() {
        let ten = document.getElementById('hoTen').value.trim();
        let lop = document.getElementById('tenLop').value;

        if (ten === "" || lop === "") {
            alert("Please enter your Full Name and Class to begin!");
            return;
        }

        document.getElementById('display-name').innerText = ten;
        document.getElementById('display-class').innerText = lop;

        document.getElementById('login-screen').style.display = "none";
        document.getElementById('main-app').style.display = "block";
        
        startTimer();

        updateTab1();
        updateTab2();
        drawTab3Background();
        drawTab4Background();
    }

    // --- TAB NAVIGATION ---
    function openTab(evt, tabName) {
        let i, tabcontent, tablinks;
        tabcontent = document.getElementsByClassName("tab-content");
        for (i = 0; i < tabcontent.length; i++) {
            tabcontent[i].classList.remove("active");
        }
        tablinks = document.getElementsByClassName("tab-btn");
        for (i = 0; i < tablinks.length; i++) {
            tablinks[i].classList.remove("active");
        }
        document.getElementById(tabName).classList.add("active");
        evt.currentTarget.classList.add("active");

        if(tabName === 'Tab1') updateTab1();
        if(tabName === 'Tab2') updateTab2();
        if(tabName === 'Tab3') drawTab3Background();
        if(tabName === 'Tab4') drawTab4Background();
    }

    // --- UTILITY ---
    const centerX = 400; 
    const centerY = 200; 
    const centerAxisX = 400;

    function drawPoint(ctx, x, y, color, label, textColor = '#1e2633') {
        ctx.beginPath();
        ctx.arc(x, y, 6, 0, 2 * Math.PI);
        ctx.fillStyle = color;
        ctx.fill();
        ctx.strokeStyle = '#fff';
        ctx.lineWidth = 2;
        ctx.stroke();
        
        if (label) {
            ctx.fillStyle = textColor;
            ctx.font = 'bold 16px Arial';
            ctx.fillText(label, x + 10, y - 10);
        }
    }

    // ==========================================
    // --- TAB 1: LOCUS ---
    // ==========================================
    const canvas1 = document.getElementById('canvasTab1');
    const ctx1 = canvas1.getContext('2d');
    let trail1 = [];
    let isDragging1 = false;
    let angleP1 = 0;

    function updateTab1() {
        const R = parseInt(document.getElementById('radiusSlider1').value);
        document.getElementById('rValue1').innerText = R;
        drawTab1(R);
    }

    function clearTrail1() {
        trail1 = [];
        updateTab1();
    }

    function drawTab1(R) {
        ctx1.clearRect(0, 0, canvas1.width, canvas1.height);

        ctx1.fillStyle = 'rgba(52, 152, 219, 0.4)';
        for (let pt of trail1) {
            ctx1.beginPath();
            ctx1.arc(pt.x, pt.y, 4, 0, 2 * Math.PI);
            ctx1.fill();
        }

        let px = centerX + R * Math.cos(angleP1);
        let py = centerY + R * Math.sin(angleP1);

        ctx1.beginPath();
        ctx1.moveTo(centerX, centerY);
        ctx1.lineTo(px, py);
        ctx1.strokeStyle = '#7f8c8d';
        ctx1.setLineDash([5, 5]);
        ctx1.stroke();
        ctx1.setLineDash([]);

        drawPoint(ctx1, centerX, centerY, '#e74c3c', 'O');
        drawPoint(ctx1, px, py, '#3498db', 'P');

        ctx1.fillStyle = '#2c3e50';
        ctx1.font = 'bold 14px Arial';
        ctx1.fillText(`OP = ${R}`, (centerX + px)/2 + 5, (centerY + py)/2 - 10);
    }

    canvas1.addEventListener('mousedown', (e) => { isDragging1 = true; updateAngleP1(e); });
    canvas1.addEventListener('mousemove', (e) => {
        if (isDragging1) {
            updateAngleP1(e);
            const R = parseInt(document.getElementById('radiusSlider1').value);
            let px = centerX + R * Math.cos(angleP1);
            let py = centerY + R * Math.sin(angleP1);
            trail1.push({x: px, y: py});
            updateTab1();
        }
    });
    window.addEventListener('mouseup', () => { isDragging1 = false; });

    function updateAngleP1(e) {
        const rect = canvas1.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        angleP1 = Math.atan2(mouseY - centerY, mouseX - centerX);
        updateTab1();
    }

    // ==========================================
    // --- TAB 2: INTERSECTION ---
    // ==========================================
    const canvas2 = document.getElementById('canvasTab2');
    const ctx2 = canvas2.getContext('2d');
    let isDragging2 = false;
    let pointM = { x: 500, y: 120 };

    function updateTab2() {
        const R = parseInt(document.getElementById('radiusSlider2').value);
        document.getElementById('rValue2').innerText = R;
        
        let dx = pointM.x - centerX;
        let dy = pointM.y - centerY;
        let OM = Math.sqrt(dx*dx + dy*dy);

        if (Math.abs(OM - R) < 8 && isDragging2) {
            let angleM = Math.atan2(dy, dx);
            pointM.x = centerX + R * Math.cos(angleM);
            pointM.y = centerY + R * Math.sin(angleM);
            OM = R;
        }

        let omRounded = (OM === R) ? R : OM.toFixed(1);
        document.getElementById('omValue').innerText = omRounded;

        drawTab2(R, OM);
        updateResult2(OM, R);
    }

    function drawTab2(R, OM) {
        ctx2.clearRect(0, 0, canvas2.width, canvas2.height);

        ctx2.beginPath();
        ctx2.arc(centerX, centerY, R, 0, 2 * Math.PI);
        ctx2.strokeStyle = '#3498db';
        ctx2.lineWidth = 2;
        ctx2.stroke();
        ctx2.lineWidth = 1;

        ctx2.beginPath();
        ctx2.moveTo(centerX, centerY);
        ctx2.lineTo(pointM.x, pointM.y);
        ctx2.strokeStyle = '#e67e22';
        ctx2.setLineDash([6, 6]);
        ctx2.lineWidth = 2;
        ctx2.stroke();
        ctx2.setLineDash([]);
        ctx2.lineWidth = 1;

        drawPoint(ctx2, centerX, centerY, '#e74c3c', 'O');
        drawPoint(ctx2, pointM.x, pointM.y, '#f39c12', 'M');
    }

    function updateResult2(OM, R) {
        const box = document.getElementById('ketLuanBox');
        if (OM < R) {
            box.className = "result-box result-trong";
            box.innerHTML = "Conclusion: Point M is <b>INSIDE</b> the circle (O)";
        } else if (OM === R) {
            box.className = "result-box result-tren";
            box.innerHTML = "Conclusion: Point M is <b>ON</b> the circle (O)";
        } else {
            box.className = "result-box result-ngoai";
            box.innerHTML = "Conclusion: Point M is <b>OUTSIDE</b> the circle (O)";
        }
    }

    canvas2.addEventListener('mousedown', (e) => {
        const rect = canvas2.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        if (Math.hypot(mouseX - pointM.x, mouseY - pointM.y) < 25) {
            isDragging2 = true;
        }
    });

    canvas2.addEventListener('mousemove', (e) => {
        if (isDragging2) {
            const rect = canvas2.getBoundingClientRect();
            pointM.x = e.clientX - rect.left;
            pointM.y = e.clientY - rect.top;
            updateTab2();
        }
    });

    window.addEventListener('mouseup', () => { isDragging2 = false; });

    // ==========================================
    // --- TAB 3: LINE SYMMETRY ---
    // ==========================================
    const canvas3 = document.getElementById('canvasTab3');
    const ctx3 = canvas3.getContext('2d');
    let isTracing = false;
    let tracePoints = []; 
    let currentMousePos = null;

    function drawLeafBackground() {
        ctx3.save();
        ctx3.translate(centerAxisX, 250);
        ctx3.scale(1.5, 1.5);
        ctx3.beginPath();
        
        ctx3.moveTo(0, 100);    
        ctx3.lineTo(5, 100);
        ctx3.lineTo(2, 40);
        ctx3.lineTo(40, 50);    
        ctx3.lineTo(30, 10);
        ctx3.lineTo(80, -20);   
        ctx3.lineTo(40, -40);
        ctx3.lineTo(60, -90);   
        ctx3.lineTo(20, -70);
        ctx3.lineTo(0, -120);   
        
        ctx3.lineTo(-20, -70);
        ctx3.lineTo(-60, -90);
        ctx3.lineTo(-40, -40);
        ctx3.lineTo(-80, -20);
        ctx3.lineTo(-30, 10);
        ctx3.lineTo(-40, 50);
        ctx3.lineTo(-2, 40);
        ctx3.lineTo(-5, 100);
        
        ctx3.closePath();
        
        ctx3.fillStyle = 'rgba(230, 126, 34, 0.2)';
        ctx3.fill();
        ctx3.lineWidth = 2;
        ctx3.strokeStyle = 'rgba(211, 84, 0, 0.4)';
        ctx3.stroke();
        ctx3.restore();
    }

    function drawTab3Background() {
        ctx3.clearRect(0, 0, canvas3.width, canvas3.height);
        
        drawLeafBackground();

        ctx3.beginPath();
        ctx3.moveTo(centerAxisX, 20);
        ctx3.lineTo(centerAxisX, canvas3.height - 20);
        ctx3.strokeStyle = '#2c3e50';
        ctx3.setLineDash([8, 8]);
        ctx3.lineWidth = 2;
        ctx3.stroke();
        ctx3.setLineDash([]);
        
        ctx3.fillStyle = '#2c3e50';
        ctx3.font = 'bold 18px Arial';
        ctx3.fillText('Δ', centerAxisX + 10, 30);

        if (tracePoints.length > 0) {
            ctx3.beginPath();
            ctx3.moveTo(tracePoints[0].x, tracePoints[0].y);
            for(let i=1; i<tracePoints.length; i++) {
                ctx3.lineTo(tracePoints[i].x, tracePoints[i].y);
            }
            ctx3.strokeStyle = '#6c5ce7';
            ctx3.lineWidth = 3;
            ctx3.stroke();

            ctx3.beginPath();
            ctx3.moveTo(mirrorX(tracePoints[0].x), tracePoints[0].y);
            for(let i=1; i<tracePoints.length; i++) {
                ctx3.lineTo(mirrorX(tracePoints[i].x), tracePoints[i].y);
            }
            ctx3.strokeStyle = '#27ae60';
            ctx3.lineWidth = 3;
            ctx3.stroke();
        }

        if (currentMousePos) {
            let mX = currentMousePos.x;
            let mY = currentMousePos.y;
            let symX = mirrorX(mX);

            ctx3.beginPath();
            ctx3.moveTo(mX, mY);
            ctx3.lineTo(symX, mY);
            ctx3.strokeStyle = '#e74c3c';
            ctx3.setLineDash([4, 4]);
            ctx3.lineWidth = 1;
            ctx3.stroke();
            ctx3.setLineDash([]);

            ctx3.fillStyle = '#e74c3c';
            ctx3.fillRect(centerAxisX - 4, mY - 4, 8, 8);

            drawPoint(ctx3, mX, mY, '#6c5ce7', 'A');
            drawPoint(ctx3, symX, mY, '#27ae60', "A'");

            let distance = Math.abs(mX - centerAxisX).toFixed(1);
            document.getElementById('distanceDisplay').innerHTML = `d(A, Δ) = ${distance} px<br>d(A', Δ) = ${distance} px`;
        }
    }

    function mirrorX(x) { return centerAxisX + (centerAxisX - x); }

    function clearTrail3() {
        tracePoints = [];
        currentMousePos = null;
        document.getElementById('distanceDisplay').innerHTML = `d(A, Δ) = 0.0 px<br>d(A', Δ) = 0.0 px`;
        drawTab3Background();
    }

    canvas3.addEventListener('mousedown', (e) => { isTracing = true; tracePoints = []; updateTrace3(e); });
    canvas3.addEventListener('mousemove', (e) => {
        if (isTracing) updateTrace3(e);
        else {
            const rect = canvas3.getBoundingClientRect();
            currentMousePos = { x: e.clientX - rect.left, y: e.clientY - rect.top };
            drawTab3Background();
        }
    });
    window.addEventListener('mouseup', () => { isTracing = false; });
    canvas3.addEventListener('mouseleave', () => { isTracing = false; currentMousePos = null; drawTab3Background(); });

    function updateTrace3(e) {
        const rect = canvas3.getBoundingClientRect();
        currentMousePos = { x: e.clientX - rect.left, y: e.clientY - rect.top };
        tracePoints.push(currentMousePos);
        drawTab3Background();
    }

    // ==========================================
    // --- TAB 4: POINT SYMMETRY ---
    // ==========================================
    const canvas4 = document.getElementById('canvasTab4');
    const ctx4 = canvas4.getContext('2d');
    let isTracing4 = false;
    let tracePoints4 = []; 
    let currentMousePos4 = null;
    const centerPointY = 225; // Tâm O của canvas 4

    function drawPinwheelBackground() {
        ctx4.save();
        ctx4.translate(centerAxisX, centerPointY);
        for(let i = 0; i < 4; i++) {
            ctx4.beginPath();
            ctx4.moveTo(0, 0);
            ctx4.quadraticCurveTo(60, -30, 100, -100);
            ctx4.quadraticCurveTo(30, -60, 0, 0);
            ctx4.fillStyle = (i % 2 === 0) ? 'rgba(52, 152, 219, 0.2)' : 'rgba(155, 89, 182, 0.2)';
            ctx4.fill();
            ctx4.strokeStyle = 'rgba(41, 128, 185, 0.4)';
            ctx4.stroke();
            ctx4.rotate(Math.PI / 2);
        }
        ctx4.restore();
    }

    function drawTab4Background() {
        ctx4.clearRect(0, 0, canvas4.width, canvas4.height);
        
        drawPinwheelBackground();

        // Tâm đối xứng O
        drawPoint(ctx4, centerAxisX, centerPointY, '#e74c3c', 'O', '#e74c3c');

        if (tracePoints4.length > 0) {
            // Original trace
            ctx4.beginPath();
            ctx4.moveTo(tracePoints4[0].x, tracePoints4[0].y);
            for(let i=1; i<tracePoints4.length; i++) {
                ctx4.lineTo(tracePoints4[i].x, tracePoints4[i].y);
            }
            ctx4.strokeStyle = '#6c5ce7';
            ctx4.lineWidth = 3;
            ctx4.stroke();

            // Point-symmetric trace
            ctx4.beginPath();
            let symStart = mirrorPoint(tracePoints4[0].x, tracePoints4[0].y);
            ctx4.moveTo(symStart.x, symStart.y);
            for(let i=1; i<tracePoints4.length; i++) {
                let symP = mirrorPoint(tracePoints4[i].x, tracePoints4[i].y);
                ctx4.lineTo(symP.x, symP.y);
            }
            ctx4.strokeStyle = '#e67e22';
            ctx4.lineWidth = 3;
            ctx4.stroke();
        }

        if (currentMousePos4) {
            let mX = currentMousePos4.x;
            let mY = currentMousePos4.y;
            let symP = mirrorPoint(mX, mY);

            // Connect A to A' through O
            ctx4.beginPath();
            ctx4.moveTo(mX, mY);
            ctx4.lineTo(symP.x, symP.y);
            ctx4.strokeStyle = '#7f8c8d';
            ctx4.setLineDash([5, 5]);
            ctx4.lineWidth = 1;
            ctx4.stroke();
            ctx4.setLineDash([]);

            drawPoint(ctx4, mX, mY, '#6c5ce7', 'A');
            drawPoint(ctx4, symP.x, symP.y, '#e67e22', "A'");

            let distance = Math.hypot(mX - centerAxisX, mY - centerPointY).toFixed(1);
            document.getElementById('distanceDisplay4').innerHTML = `d(A, O) = ${distance} px<br>d(A', O) = ${distance} px`;
        }
    }

    function mirrorPoint(x, y) {
        return {
            x: centerAxisX + (centerAxisX - x),
            y: centerPointY + (centerPointY - y)
        };
    }

    function clearTrail4() {
        tracePoints4 = [];
        currentMousePos4 = null;
        document.getElementById('distanceDisplay4').innerHTML = `d(A, O) = 0.0 px<br>d(A', O) = 0.0 px`;
        drawTab4Background();
    }

    canvas4.addEventListener('mousedown', (e) => { isTracing4 = true; tracePoints4 = []; updateTrace4(e); });
    canvas4.addEventListener('mousemove', (e) => {
        if (isTracing4) updateTrace4(e);
        else {
            const rect = canvas4.getBoundingClientRect();
            currentMousePos4 = { x: e.clientX - rect.left, y: e.clientY - rect.top };
            drawTab4Background();
        }
    });
    window.addEventListener('mouseup', () => { isTracing4 = false; });
    canvas4.addEventListener('mouseleave', () => { isTracing4 = false; currentMousePos4 = null; drawTab4Background(); });

    function updateTrace4(e) {
        const rect = canvas4.getBoundingClientRect();
        currentMousePos4 = { x: e.clientX - rect.left, y: e.clientY - rect.top };
        tracePoints4.push(currentMousePos4);
        drawTab4Background();
    }

</script>
</body>
</html>
