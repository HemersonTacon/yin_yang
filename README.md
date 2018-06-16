# yin_yang
Exploring canvas and trigonometry

<!DOCTYPE html>
<html>
<body>
	<center>
		<canvas id="myCanvas" width="500" height="500" style="border:1px solid #d3d3d3;">
		Your browser does not support the HTML5 canvas tag.</canvas>
	
		<br><br>
	
		<h4 id="RPM">Velocidade de rotação: 60 RPM</h4>
		<input type=range id="speed" oninput="updateRPM()">
		</input>
	</center>
	<script>
	var c = document.getElementById("myCanvas");
	var context = c.getContext("2d");
	var fps = 60;
	// 1000ms divided by frame per second to know how often (in which time interval) I need to update the draw
	var update_rate = 1000/fps;
	// Which angle I need to increase in offset to complete 1 rotation per second which implies 60RPM
	var step = 2*Math.PI/(fps);
	var offset = 0;
	// RPM speed factor, 1 implies 60 RPM
	var speed = 1;
	var size = 1;

	var updateRPM = function(){

		speed = 2 * document.getElementById("speed").value/100;
		document.getElementById("RPM").innerHTML  = "Velocidade de rotação: "+ (speed*60).toFixed(2) +" RPM";

	}

	var draw = function(){
		context.clearRect(0, 0, c.width, c.height);
		
		//yin
		context.beginPath();
		context.arc(250, 250, 100, -Math.PI/2 + offset, Math.PI/2 + offset);
		context.arc(250 + Math.cos(offset + Math.PI/2)*50, 300 - (1 - Math.sin(offset + Math.PI/2))*50, 50, Math.PI/2 + offset, 3*Math.PI/2 + offset);
		context.arc(250 - Math.cos(offset + Math.PI/2)*50, 200 + (1 - Math.sin(offset + Math.PI/2))*50, 50, Math.PI/2 + offset, -Math.PI/2 + offset, true);
		context.fillStyle="black";
		context.fill();
		context.stroke();

		//yang
		context.beginPath();
		context.arc(250, 250, 100, -Math.PI/2 + offset, Math.PI/2 + offset, true);
		context.stroke();

		//yin interno
		context.beginPath();
		context.arc(250 - Math.cos(offset + Math.PI/2)*50, 200 + (1 - Math.sin(offset + Math.PI/2))*50, 10, 0, 2*Math.PI);
		context.fillStyle="black";
		context.fill();

		//yang interno
		context.beginPath();
		context.arc(250 + Math.cos(offset + Math.PI/2)*50, 300 - (1 - Math.sin(offset + Math.PI/2))*50 , 10, 0, 2*Math.PI);
		context.fillStyle="white";
		context.fill();
		
		offset = (offset + step*speed)%(2*Math.PI);
		//console.log("offset: "+offset+" step: "+step);
		setTimeout(draw, update_rate);
	}

	draw();
	</script> 

</body>
</html>
