Here’s a simple gaming website template using HTML, CSS, and JavaScript. This example includes:

A homepage with a game section

A navigation menu

A simple embedded browser game (Flappy Bird clone)


1. Create index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Gaming Website</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Welcome to My Gaming Website</h1>
        <nav>
            <ul>
                <li><a href="#">Home</a></li>
                <li><a href="#">Games</a></li>
                <li><a href="#">About</a></li>
                <li><a href="#">Contact</a></li>
            </ul>
        </nav>
    </header>

    <section class="game-section">
        <h2>Play Flappy Bird</h2>
        <canvas id="gameCanvas"></canvas>
        <script src="game.js"></script>
    </section>

    <footer>
        <p>© 2025 My Gaming Website. All rights reserved.</p>
    </footer>
</body>
</html>

2. Create styles.css

body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
    background-color: #222;
    color: white;
}

header {
    background: #333;
    padding: 15px;
}

nav ul {
    list-style: none;
    padding: 0;
}

nav ul li {
    display: inline;
    margin: 0 15px;
}

nav ul li a {
    color: white;
    text-decoration: none;
}

.game-section {
    margin: 20px;
}

canvas {
    background: lightblue;
    display: block;
    margin: auto;
}

footer {
    background: #111;
    padding: 10px;
    margin-top: 20px;
}

3. Create game.js (Simple Flappy Bird Clone)

const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

canvas.width = 400;
canvas.height = 500;

let bird = { x: 50, y: 200, width: 20, height: 20, gravity: 0, jump: -5 };
let pipes = [];
let gameOver = false;

document.addEventListener("keydown", () => { bird.gravity = bird.jump; });

function update() {
    if (gameOver) return;

    bird.gravity += 0.2;
    bird.y += bird.gravity;

    if (bird.y >= canvas.height || bird.y <= 0) gameOver = true;

    if (pipes.length < 1 || pipes[pipes.length - 1].x < 250) {
        let pipeY = Math.random() * (canvas.height - 150);
        pipes.push({ x: canvas.width, y: pipeY, width: 40, height: 150 });
    }

    pipes.forEach(pipe => {
        pipe.x -= 2;
        if (bird.x < pipe.x + pipe.width && bird.x + bird.width > pipe.x &&
            (bird.y < pipe.y || bird.y + bird.height > pipe.y + pipe.height)) {
            gameOver = true;
        }
    });

    pipes = pipes.filter(pipe => pipe.x > -50);
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "yellow";
    ctx.fillRect(bird.x, bird.y, bird.width, bird.height);

    ctx.fillStyle = "green";
    pipes.forEach(pipe => {
        ctx.fillRect(pipe.x, 0, pipe.width, pipe.y);
        ctx.fillRect(pipe.x, pipe.y + pipe.height, pipe.width, canvas.height);
    });

    if (gameOver) {
        ctx.fillStyle = "red";
        ctx.font = "30px Arial";
        ctx.fillText("Game Over!", 120, 250);
    }
}

function gameLoop() {
    update();
    draw();
    requestAnimationFrame(gameLoop);
}

gameLoop();


---

How to Host It for Free?

1. Use GitHub Pages (Best for free hosting)

Create a GitHub repository

Upload your index.html, styles.css, and game.js

Go to Settings > Pages and enable GitHub Pages



2. Use Netlify or Vercel (Free static website hosting)

Sign up

Upload your files

Get a free link to your site




Would you like help setting up GitHub Pages or Netlify?

