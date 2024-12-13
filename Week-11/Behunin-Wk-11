// Django Behunin - Mart 120 Creative Code -Professor Cassens - 11-12-2024

//Week 11 "Homework 11"


let player, obstacles = [], staticObstacle, exit;
let gameWon = false;

function setup() {
  createCanvas(600, 400);

  player = createPlayer(50, height / 2, 20, 3);
  exit = createExit(width - 50, height / 2 - 20, 40, 80);

  for (let i = 0; i < 2; i++) {
    obstacles.push(createObstacle(random(width), random(height), random(30, 50)));
  }
}

function draw() {
  background(220);

  if (!gameWon) {
    displayPlayer();
    movePlayer();
    checkCollision();
  }

  moveAndDisplayObstacles();
  if (staticObstacle) displayStaticObstacle();

  displayExit();
  checkWinCondition();
}

function createPlayer(x, y, size, speed) {
  return { x, y, size, speed, startX: x, startY: y };
}

function createExit(x, y, w, h) {
  return { x, y, w, h };
}

function createObstacle(x, y, size) {
  return {
    x, y, size, color: color(random(255), random(255), random(255)),
    xSpeed: random(-2, 2), ySpeed: random(-2, 2)
  };
}

function displayPlayer() {
  fill(0, 0, 255);
  rect(player.x, player.y, player.size, player.size);
}

function movePlayer() {
  if (keyIsDown(LEFT_ARROW) || keyIsDown(65)) player.x -= player.speed;
  if (keyIsDown(RIGHT_ARROW) || keyIsDown(68)) player.x += player.speed;
  if (keyIsDown(UP_ARROW) || keyIsDown(87)) player.y -= player.speed;
  if (keyIsDown(DOWN_ARROW) || keyIsDown(83)) player.y += player.speed;

  // Boundary checks using if/else if structures
  if (player.x < 0) {
    player.x = 0;
  } else if (player.x > width - player.size) {
    player.x = width - player.size;
  }

  if (player.y < 0) {
    player.y = 0;
  } else if (player.y > height - player.size) {
    player.y = height - player.size;
  }
}

function moveAndDisplayObstacles() {
  for (let obstacle of obstacles) {
    fill(obstacle.color);
    ellipse(obstacle.x, obstacle.y, obstacle.size);
    obstacle.x += obstacle.xSpeed;
    obstacle.y += obstacle.ySpeed;

    // Wrap obstacles around canvas with if/else if structures
    if (obstacle.x > width) {
      obstacle.x = 0;
    } else if (obstacle.x < 0) {
      obstacle.x = width;
    }

    if (obstacle.y > height) {
      obstacle.y = 0;
    } else if (obstacle.y < 0) {
      obstacle.y = height;
    }
  }
}

function displayStaticObstacle() {
  fill(150, 75, 0);
  rect(staticObstacle.x, staticObstacle.y, staticObstacle.size, staticObstacle.size);
}

function displayExit() {
  fill(0, 255, 0);
  rect(exit.x, exit.y, exit.w, exit.h);
}

function checkCollision() {
  for (let obstacle of obstacles) {
    if (dist(player.x, player.y, obstacle.x, obstacle.y) < player.size / 2 + obstacle.size / 2) {
      resetPlayer();
    }
  }
  if (staticObstacle && dist(player.x, player.y, staticObstacle.x + staticObstacle.size / 2, staticObstacle.y + staticObstacle.size / 2) < player.size / 2 + staticObstacle.size / 2) {
    resetPlayer();
  }
}

function resetPlayer() {
  player.x = player.startX;
  player.y = player.startY;
}

function checkWinCondition() {
  if (!gameWon && player.x + player.size >= exit.x && player.y + player.size >= exit.y && player.y <= exit.y + exit.h) {
    gameWon = true;
    textSize(32);
    fill(0);
    textAlign(CENTER, CENTER);
    text("You Won!", width / 2, height / 2);
  }
}

function mousePressed() {
  if (!staticObstacle) {
    staticObstacle = { x: mouseX, y: mouseY, size: 30 };
  }
}
