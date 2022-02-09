<button id="button" onclick="createBall();"
style="
z-index: 2;
position: absolute;
left: 150px;
top: 350px;
width: 150px;
height: 75px;
background-color: darkcyan;">Make a ball!</button>
<button hidden id="stop" onclick="clearBalls()"
style="
z-index: 2;
position: absolute;
left: 0px;
top: 350px;
width: 150px;
height: 75px;
background-color: darkcyan;">Goodbye, balls!</button>
<script>



let red = Math.floor(Math.random()*255);
let green = Math.floor(Math.random()*255);
let blue = Math.floor(Math.random()*255);
var xMin = 0;
var yMin = 0;
var xMax = 300;
var yMax = 300;
var ballList = [];
var ballDiv;
var BallI;

function moveBall() {
  for (let i = 0; i < ballList.length; i++){
    ballI = ballList[i];
    ballDiv = document.getElementById(`ball${i}`)
    ballI.positionX += ballI.velocityX;
    ballDiv.style.left = ballI.positionX + 'px';
    if (ballI.positionX >= xMax || ballI.positionX <= xMin){
      ballI.velocityX = -ballI.velocityX;
      changeColor(ballDiv);
    }
    ballI.positionY += ballI.velocityY;
    ballDiv.style.top = ballI.positionY + 'px';
    if (ballI.positionY >= yMax || ballI.positionY <= yMin){
      ballI.velocityY = -ballI.velocityY;
      changeColor(ballDiv);
    }
  }
}

function changeColor(changingBall) {
  //chooses random rgb values
  red = Math.floor(Math.random()*255);
  green = Math.floor(Math.random()*255);
  blue = Math.floor(Math.random()*255);
  //and sets the ball's background color to those values
  changingBall.style.background = `rgb(${red},${green},${blue})`
}

function createBall(){
  var ball = {
    id : ballList.length,
    velocityX : Math.floor((Math.random()*15)+1),
    velocityY : Math.floor((Math.random()*15)+1),
    positionX : Math.floor((Math.random()*300)),
    positionY : Math.floor((Math.random()*300)),
    color : `rgb(${red},${green},${blue})`
  }
  ballList.push(ball);
  var div = document.createElement('div');
  div.id = `ball${ball.id}`;
  div.style.zIndex = '1';
  div.style.position = 'absolute';
  div.style.left = ball.positionX + 'px';
  div.style.top = ball.positionY + 'px';
  div.style.width = '50px';
  div.style.height = '50px';
  div.style.borderRadius = '50%';
  div.style.background = ball.color;
  document.getElementsByTagName('body')[0].appendChild(div);
  document.getElementById('button').innerHTML = 'Make another ball!';
  changeColor(div);
  document.getElementById('stop').hidden = false;
}
function clearBalls(){
  for (let j = 0; j < ballList.length; j++){
    ballDiv = document.getElementById(`ball${j}`);
    ballDiv.remove();
  }
  ballList = [];
  document.getElementById('button').innerHTML = 'Make a ball!';
  document.getElementById('stop').hidden = true;
}
setInterval(moveBall, 50);
</script>
