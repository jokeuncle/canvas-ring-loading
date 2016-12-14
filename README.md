# canvas-ring-loading
canvas 环形进度条
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		.box{
			width: 400px;
			height: 400px;
			margin: 50px auto;
			box-shadow: -3px -3px 3px rgba(0,0,0,.6),5px 5px 5px rgba(0,0,0,.5);
		}
	</style>
</head>
<body>
	<div class="box">
		<canvas id="canvas" width="400" height="400"></canvas>
	</div>
	<script>
		var canvas=document.querySelector('#canvas');
		var ctx=canvas.getContext('2d');
		var start={
			x:0,      //起始点的x坐标
			y:-115    //起始点的y坐标
		}
		var startTime=new Date();
		var x=start.x;
		var y=start.y;
		var r=10;     //every single point's radius
		var step=0.5; //control the frequency of drawing point or the num of the point
		var timer;    //control the end of painting
		var ctrl1=1;
		function init(){
				ctx.translate(200,200);
				ctx.beginPath();
				ctx.arc(0,0,110,0,Math.PI*2);
				ctx.stroke();
				ctx.beginPath();
				ctx.arc(0,0,120,0,Math.PI*2);
				ctx.stroke();
		}
		function paint(x,y,r){
			ctx.beginPath();
			ctx.arc(x,y,r,0,Math.PI*2);
			ctx.fillStyle="red";
			ctx.fill();
		}
		function calculateY(){
			return Math.sqrt(Math.pow(115,2)-Math.pow(x,2));
		}
		function update(){
			if(x>-115 && ctrl1){
				x-=step;
				y=-calculateY(x);
			}else if(x>=115){
				ctrl1=1;
			}else if(x<=-115){
				ctrl1=0;
				x+=step;
				y=calculateY(x);
			}else if(x<115){
				x+=step;
				y=calculateY(x);
			}
		}
		function loading_app(){
			init();
			paint(start.x,start.y);
			timer=setInterval(function(){
			if(new Date()-startTime>=22000){
				clearInterval(timer);
			}	
				update();
				paint(x,y,r);
			},20)
		}
	</script>
</body>
</html>
