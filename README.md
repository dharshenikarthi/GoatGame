# Project Responsive Web Design using Bootstrap
## Date:15.12.24

## AIM:
To create a simplified goat game.


## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Insert the necessary CSS and JavaScript files as external in order to use Bootstrap.

### Step 5:
Create a HTML file and include the needed Bootstrap components.

### Step 6:
Publish the website in the LocalHost.

## PROGRAM :
index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Goat Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="game-area">
        <div class="road">
            <div class="goat" id="goat">
                <img src="goat.png" alt="">
            </div>
            <div class="object leaf" id="leaf">
                <img src="leaf.png" alt="">
            </div>
            <div class="object bike" id="bike">
                <img src="bike.png" alt="">
            </div>
        </div>
    </div>
    <div class="score">Score: <span id="score">0</span></div>
    <script src="script.js"></script>
</body>
</html>

```
script.js
```
const goat = document.getElementById('goat');
const leaf = document.getElementById('leaf');
const bike = document.getElementById('bike');
const scoreDisplay = document.getElementById('score');
let score = 0;
let goatPosition = 125; // Starting position of the goat
let gameInterval;
let gameSpeed = 5; // Speed of object movement

document.addEventListener('keydown', (event) => {
    if (event.key === 'ArrowLeft' && goatPosition > 0) {
        goatPosition -= 20;
    } else if (event.key === 'ArrowRight' && goatPosition < 250) {
        goatPosition += 20;
    }
    goat.style.left = `${goatPosition}px`;
});

function startGame() {
    // Place initial objects randomly
    resetObject(leaf, 'leaf');
    resetObject(bike, 'bike');

    gameInterval = setInterval(() => {
        moveObject(leaf, 'leaf');
        moveObject(bike, 'bike');
        checkCollision();
    }, 20);
}

function moveObject(object, type) {
    let objectTop = parseInt(window.getComputedStyle(object).getPropertyValue('top'));

    if (objectTop >= 600) { // If object goes off the screen, reset it
        resetObject(object, type);
    } else {
        object.style.top = `${objectTop + gameSpeed}px`;
    }
}

function resetObject(object, type) {
    object.style.top = '-50px'; // Start off screen at the top
    object.style.left = `${Math.floor(Math.random() * 270)}px`; // Random X position
}

function checkCollision() {
    let goatRect = goat.getBoundingClientRect();
    let leafRect = leaf.getBoundingClientRect();
    let bikeRect = bike.getBoundingClientRect();

    // Check collision with leaf
    if (goatRect.left < leafRect.right &&
        goatRect.right > leafRect.left &&
        goatRect.top < leafRect.bottom &&
        goatRect.bottom > leafRect.top) {
        score++;
        scoreDisplay.textContent = score;
        resetObject(leaf, 'leaf');
    }

    // Check collision with bike
    if (goatRect.left < bikeRect.right &&
        goatRect.right > bikeRect.left &&
        goatRect.top < bikeRect.bottom &&
        goatRect.bottom > bikeRect.top) {
        clearInterval(gameInterval);
        alert('Game Over! Your Score: ' + score);
        window.location.reload();
    }
}

startGame();

```
style.css
```

body {
    margin: 0;
    overflow: hidden;
    background-color: #f0f0f0;
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
}

.game-area {
    position: relative;
    width: 300px;
    height: 600px;
    border: 5px solid #333;
    overflow: hidden;
    background-color: #222;
}

.road {
    position: absolute;
    width: 100%;
    height: 100%;
    /* background-image: linear-gradient(to bottom, #444 10%, #555 90%);
    animation: moveRoad 1s linear infinite; */
    background-size: 100% 100%;
    background-image: url("./assets/road.jpg");
}

/* @keyframes moveRoad {
    0% { background-position-y: 0; }
    100% { background-position-y: 100%; }
} */

.goat {
    position: absolute;
    width: 50px;
    height: 80px;
    /* background-color: blue; */
    bottom: 20px;
    left: 125px;
    border-radius: 50%;
    display: flex;
}

.goat img {
    transform: scale(2);
}

.object {
    position: absolute;
    width: 70px;
    height: 150px;
    top: -50px; /* Start off screen */
}

.leaf {
    /* background-color: gold; */
    border-radius: 50%;
    display: flex;
}

.bike {
    /* background-color: red; */
    border-radius: 10%;
    display: flex;
}

.score {
    font-size: 20px;
    margin-top: 20px;
    color: white;
    background-color: #333;
    padding: 5px 10px;
}

```
## OUTPUT:

![Screenshot 2024-12-28 182207](https://github.com/user-attachments/assets/07f0b5ee-4671-4671-b69b-79015f10220c)
