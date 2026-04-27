<!DOCTYPE html>
<html>
<head>
    <title>لعبتي الأولى</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: black;
        }
        #player {
            width: 50px;
            height: 50px;
            background: red;
            position: absolute;
            top: 100px;
            left: 100px;
        }
        .coin {
            width: 30px;
            height: 30px;
            background: yellow;
            position: absolute;
            border-radius: 50%;
        }
        #score {
            position: absolute;
            color: white;
            font-size: 20px;
            top: 10px;
            left: 10px;
        }
    </style>
</head>
<body>

<div id="player"></div>
<div id="score">Score: 0</div>

<script>
let player = document.getElementById("player");
let scoreText = document.getElementById("score");

let x = 100;
let y = 100;
let score = 0;

document.addEventListener("keydown", function(e) {
    if (e.key === "ArrowRight") x += 20;
    if (e.key === "ArrowLeft") x -= 20;
    if (e.key === "ArrowUp") y -= 20;
    if (e.key === "ArrowDown") y += 20;

    player.style.left = x + "px";
    player.style.top = y + "px";

    checkCollision();
});

function createCoin() {
    let coin = document.createElement("div");
    coin.classList.add("coin");

    coin.style.left = Math.random() * window.innerWidth + "px";
    coin.style.top = Math.random() * window.innerHeight + "px";

    document.body.appendChild(coin);
}

function checkCollision() {
    let coins = document.querySelectorAll(".coin");

    coins.forEach(coin => {
        let coinX = coin.offsetLeft;
        let coinY = coin.offsetTop;

        if (Math.abs(x - coinX) < 30 && Math.abs(y - coinY) < 30) {
            coin.remove();
            score++;
            scoreText.innerText = "Score: " + score;
            createCoin();
        }
    });
}

// إنشاء أول عملة
createCoin();
</script>

</body>
</html>
