<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MMORPG Chiến Đấu</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #2c3e50;
        }

        #game-container {
            width: 800px;
            height: 600px;
            background-color: #ecf0f1;
            position: relative;
            overflow: hidden;
            border: 2px solid #34495e;
        }

        .character {
            width: 50px;
            height: 50px;
            position: absolute;
            background-color: red;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <div id="player" class="character" style="top: 50%; left: 50%;"></div>
        <div id="enemy" class="character" style="top: 20%; left: 20%; background-color: blue;"></div>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const player = document.getElementById('player');
            const enemy = document.getElementById('enemy');
            const gameContainer = document.getElementById('game-container');
            let playerHealth = 100;
            let enemyHealth = 100;

            document.addEventListener('keydown', function(event) {
                let top = parseInt(player.style.top);
                let left = parseInt(player.style.left);

                switch(event.key) {
                    case 'ArrowUp':
                        player.style.top = (top - 10) + 'px';
                        break;
                    case 'ArrowDown':
                        player.style.top = (top + 10) + 'px';
                        break;
                    case 'ArrowLeft':
                        player.style.left = (left - 10) + 'px';
                        break;
                    case 'ArrowRight':
                        player.style.left = (left + 10) + 'px';
                        break;
                    case ' ':
                        attack();
                        break;
                }
            });

            function attack() {
                const playerRect = player.getBoundingClientRect();
                const enemyRect = enemy.getBoundingClientRect();

                if (playerRect.left < enemyRect.right &&
                    playerRect.right > enemyRect.left &&
                    playerRect.top < enemyRect.bottom &&
                    playerRect.bottom > enemyRect.top) {
                    enemyHealth -= 10;
                    console.log(`Enemy Health: ${enemyHealth}`);
                    if (enemyHealth <= 0) {
                        enemy.remove();
                        console.log('Enemy defeated!');
                    }
                }
            }
        });
    </script>
</body>
</html>
