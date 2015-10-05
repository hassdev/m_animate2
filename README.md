<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>mouse coordinates jq</title>
<style>
	html, body {
		width: 100%;
		height: 100%;
		padding: 0;
		margin: 0;
	}
	body {
		background-color: rgba(100,100,100,0.2);
		overflow: hidden;
	}

	#wrapper {
		width: 100%;
		min-height: 100%;
		margin: 0 auto;
		position: relative;
	}

	#pp {
		width: 100px;
		height: 100px;
		background-color: rgba(100,0,0,0.3);
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		margin: 0 auto;
	}

	svg {
		outline: 1px solid blue;
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		margin: 0 auto;
		width: 100%;
		height: 100%;
	}
</style>
</head>

<body>
	<div id="wrapper">
		<div id="status1"></div>
		<div id="status2"></div>
		<div id="pp"></div>
		<svg id="mysvg" height="400" width="450"></svg>
	</div><!--/#wrapper-->
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
	<script>
		$(document).ready(function(){
			var d = document;
			var mysvg = d.getElementById("mysvg");

			setInterval(function(){
				var rand_global = {
					aa: Math.floor(Math.random()*100)
				};
				$("#status2").html(rand_global.aa);
			}, 1000);

			mysvg.addEventListener("mousemove", myFunction1);

			function myFunction1(e) {
				//svg width and height
				var svgw = $("svg").width();
				var svgh = $("svg").height();

				//initial point
				var mdpt = svgw/2;
				var yini = svgh - 100;

				//aquire x and y coordinates relative to window size
				var mx = e.clientX;
				var my = e.clientY;

				var mxabs = (mx-mdpt);
				var myabs = (my-yini);

				if(mxabs <= 0) {
					mxabs = 0;
				}

				var mxabs_2

				var mxabsr = -(mx-mdpt);
				var myabsr = (my-yini);

				if(mxabsr >= 0){
					mxabsr = 0;
				}

				//random numbers
				var rand = {
					z1: Math.floor(Math.random()*10),
					z2: -Math.floor(Math.random()*10),
					aa: -(Math.floor(Math.random()*50)),
					ba: Math.floor(Math.random()*50),
					ca: -(Math.floor(Math.random()*50)),
					da: Math.floor(Math.random()*50),
					ea: -(Math.floor(Math.random()*50)),
					fa: Math.floor(Math.random()*50)
				};

				var input1 = '<path d="M ' + mdpt + ' ' + yini + 
						 ' q ' + (mxabs/8) + ',' + rand.aa + ' ' + ((mxabs/8)*2) + ',' + rand.z1 + ' ' + (mxabs/8) + ',' + rand.ba + ' ' + ((mxabs/8)*2) + ',' + rand.z2 + ' ' + (mxabs/8) + ',' + rand.ca + ' ' + ((mxabs/8)*2) + ',' + rand.z1 + ' ' + (mxabs/8) + ',' + rand.da + ' ' + ((mxabs/8)*2) + ',' + rand.z2 + 
						 //' l ' + (mxabs-100) + ' ' + 0 +
						 '" stroke="orange" stroke-width="7" stroke-linejoin="round" fill="none" />';

				var input2 = '<path d="M ' + mdpt + ' ' + yini + 
						 ' l ' + mxabsr + ' ' + 0 +
						 '" stroke="red" stroke-width="7" stroke-linejoin="round" fill="none" />';

				$("#mysvg").html(input1+input2);
				
				$("#status1").html("<strong>svg size</strong><br>width: " + svgw + "<br>height: " + svgh + "<br><br>X coord: " + mxabs + "<br>Y coord: " + myabs + "<br><br>random local: " + rand.aa + "<br><br>random global: ");
			}
		});
	</script>
</body>
</html>
