<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Drawing App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
            background: linear-gradient(45deg, #ff9a9e, #fad0c4);
            overflow: hidden;
        }

        .bounce {
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .container {
            padding: 20px;
        }

        canvas {
            border: 2px solid black;
            background: white;
        }

        .tools {
            margin-top: 10px;
        }

        button, select {
            padding: 10px;
            border: none;
            margin: 5px;
            cursor: pointer;
            border-radius: 5px;
        }

        .home-btn, .contact-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: #ff6b6b;
            color: white;
        }

        .contact-btn {
            right: 80px;
        }
    </style>
</head>
<body>
    <h1 class="bounce">Welcome to the Drawing App</h1>
    <div class="container">
        <canvas id="drawingCanvas" width="800" height="500"></canvas>
        <div class="tools">
            <input type="color" id="colorPicker">
            <select id="brushSize">
                <option value="2">Small</option>
                <option value="5">Medium</option>
                <option value="10">Large</option>
            </select>
            <button onclick="clearCanvas()">Clear</button>
        </div>
    </div>
    <button class="home-btn" onclick="location.href='index.html'">Home</button>
    <button class="contact-btn" onclick="location.href='contact.html'">Contact</button>
    
    <script>
        const canvas = document.getElementById("drawingCanvas");
        const ctx = canvas.getContext("2d");
        let painting = false;

        function startPosition(e) {
            painting = true;
            draw(e);
        }

        function endPosition() {
            painting = false;
            ctx.beginPath();
        }

        function draw(e) {
            if (!painting) return;
            ctx.lineWidth = document.getElementById("brushSize").value;
            ctx.lineCap = "round";
            ctx.strokeStyle = document.getElementById("colorPicker").value;
            
            ctx.lineTo(e.clientX - canvas.offsetLeft, e.clientY - canvas.offsetTop);
            ctx.stroke();
            ctx.beginPath();
            ctx.moveTo(e.clientX - canvas.offsetLeft, e.clientY - canvas.offsetTop);
        }

        function clearCanvas() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        }

        canvas.addEventListener("mousedown", startPosition);
        canvas.addEventListener("mouseup", endPosition);
        canvas.addEventListener("mousemove", draw);
    </script>
</body>
</html>
