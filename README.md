<canvas id="canvas" height="400" width="800"></canvas>
<script type="text/javascript">


  window.onload = function(){
    document.addEventListener("keydown",keypush);
  }


  py=px=10;
  gs=20;
  atas=kiri=0;
  kotak = 5;
  apelX = 11;
  apelY = 11;
  score = 0;
  ganda = [];
  canvas = document.getElementById('canvas');
  ctx = canvas.getContext('2d');








  function keypush(e){
    // alert(e.keyCode);
    switch (e.keyCode) {
      case 38:
        atas = -1; kiri=0;
        break;
      case 37:
        atas = 0 ; kiri =-1;
        break;
      case 39:
        atas =0; kiri = 1;
        break;
      case 40:
        atas = 1; kiri = 0;
        break;


    }
  }




var background = new Image();
    background.src = '../orang.jpg';




function game(){
  px += kiri;
  py += atas;
  // speed++;
  console.log("px :"+px);
  if(px < 0){
    px = canvas.width/gs+15-1;
  }
  if (px > canvas.width/gs+15-1){
    px = 0;
  }


  if (py > canvas.height/gs+10-1){
    py = 0;
  }


  if (py < 0 ){
    py = canvas.height/gs+8-1;
  }


  ctx.fillStyle = "#35653f";
  ctx.fillRect(0,0,canvas.width,canvas.height);


  //apel
  ctx.beginPath();
  ctx.fillStyle = "lime";
  ctx.arc((gs-5)*apelX,(gs-5)*apelY,10,0,2*Math.PI);
  ctx.fill();
  ctx.closePath();
  if ( apelX==px && apelY==py){
    kotak++;
    score++;
    apelX = Math.floor(Math.random()*gs-1);
    apelY = Math.floor(Math.random()*gs-1);
  }
  if (apelX > canvas.width/gs-1 || apelX < 0){
    apelX = Math.floor(Math.random()*gs-1);
  }


  if (apelY > canvas.height/gs-1 || apelY < 0){
    apelX = Math.floor(Math.random()*gs-1);
  }


  ctx.font = "14px arial";
  ctx.fillText(kotak+" aplX : "+apelX+" pos px : "+px,20,80);


  //body snake
  ctx.fillStyle = "red";
  for(var i = 1; i < ganda.length; i++){
    ctx.beginPath();
    ctx.arc(ganda[i].x*(gs-5),ganda[i].y*(gs-5),gs/2,0, 2 * Math.PI);
    ctx.stroke();
    ctx.fill();
    ctx.closePath();


    if(ganda[i].x == px && ganda[i].y == py){
      kotak = 5;
      score = 0;
    }
  }


  ganda.push({x:px,y:py});
  while (ganda.length > kotak) {
    ganda.shift();
  }


  //head snake
  ctx.beginPath();
  ctx.fillStyle = "blue";
  ctx.arc(px*(gs-5),py*(gs-5),gs/2,0, 2 * Math.PI);
  ctx.fill();
  ctx.closePath();
  ctx.fillStyle = "white";
  ctx.font = "14px arial";
  ctx.fillText("Score : " + score, 400,20);


}
  setInterval(game,100);


game();
</script>
