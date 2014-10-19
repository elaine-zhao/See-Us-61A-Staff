See-Us-61A-Staff
================

//A game where you match the CS61A staff members' names to their images.

<!DOCTYPE html>
<html>
<head> How well do you know the CS61A staff? </head>

<style type="text/css">
div#memory_board{
	background:#CCC;
	border:#999 1px solid;
	width:800px;
	height:540px;
	padding:10px;
	margin:0px auto;
}
div#memory_board > div{
	background: '#CCC';
	border:#000 1px solid;
	width:71px;
	height:71px;
	float:left;
	margin:10px;
	padding:20px;
	font-size:24px;
	cursor:pointer;
	text-align:center;
	position: relative;
}
div#memory_board > div img {
	height: 100%;
}
.picture{
	background-size: cover !important
}
</style>
<script>
// Scripted By Adam khoury in connection with the following video tutorial:
// http://www.youtube.com/watch?v=c_ohDPWmsM0

var gsi_dict = {"THE GOLDEN GOD": "url('http://cs61a.org/assets/images/john-denero.jpg')", "Allen": "url('http://inst.eecs.berkeley.edu/~cs61a/fa14/assets/images/allen-nguyen.jpg')", "Andrew": "url('http://cs61a.org/assets/images/andrew-huang.jpg')", "Joy": "url('http://cs61a.org/assets/images/joy-jeng.jpg')", "Beth": "url('http://cs61a.org/assets/images/beth-marrone.jpg')", "Youri": "url('http://inst.eecs.berkeley.edu/~cs61a/fa14/assets/images/youri-park.jpg')", "Jack": "url('http://inst.eecs.berkeley.edu/~cs61a/fa14/assets/images/jack-qiao.jpg')", "Sumukh": "url('http://inst.eecs.berkeley.edu/~cs61a/fa14/assets/images/sumukh-sridhara.jpg')", "Steven": "url('http://inst.eecs.berkeley.edu/~cs61a/fa14/assets/images/steven-tang.jpg')", "Michael": "url('http://inst.eecs.berkeley.edu/~cs61a/fa14/assets/images/michael-tao.jpg')", "Dickson": "url('http://inst.eecs.berkeley.edu/~cs61a/fa14/assets/images/dickson-tsai.jpg')", "Iris": "url('http://inst.eecs.berkeley.edu/~cs61a/fa14/assets/images/iris-wang.jpg')", "Albert": "url('http://inst.eecs.berkeley.edu/~cs61a/fa14/assets/images/albert-wu.jpg')"}

var memory_array = ["THE GOLDEN GOD", gsi_dict["THE GOLDEN GOD"], "Andrew", gsi_dict["Andrew"],"Beth", gsi_dict["Beth"], "Allen", gsi_dict['Allen'], "Youri", gsi_dict['Youri'], "Joy", gsi_dict['Joy'], "Sumukh", gsi_dict['Sumukh'], "Steven", gsi_dict['Steven'], "Michael", gsi_dict['Michael'], "Dickson", gsi_dict['Dickson'], "Iris", gsi_dict['Iris'], "Albert", gsi_dict['Albert']]




//var memory_array = ['A','A','B','B','C','C','D','D','E','E','F','F','G','G','H','H','I','I','J','J','K','K','L','L'];
var memory_values = [];
var memory_tile_ids = [];
var tiles_flipped = 0;
Array.prototype.memory_tile_shuffle = function(){
    var i = this.length, j, temp;
    while(--i > 0){
        j = Math.floor(Math.random() * (i+1));
        temp = this[j];
        this[j] = this[i];
        this[i] = temp;
    }
}
function newBoard(){
	tiles_flipped = 0;
	var output = '';
    memory_array.memory_tile_shuffle();
	for(var i = 0; i < memory_array.length; i++){
		output += '<div id="tile_'+i+'" class="picture" onclick="memoryFlipTile(this, ' + i  + ')"></div>';
	}
	document.getElementById('memory_board').innerHTML = output;
}

function memoryFlipTile(tile,val){

	if(tile.innerHTML == "" && memory_values.length < 2){
		index = memory_array[val]
		

		if (memory_array[val].length > 20){

			tile.style.backgroundImage = memory_array[val];
		}
		else {
			tile.style.background = '#FFF';
			if (index == "THE GOLDEN GOD"){
				tile.innerHTML = "<div style='font-size: 20px'>" +index +"</div>"
			}
			else
			{
				tile.innerHTML = index;

			}
			
		}
				
		if(memory_values.length == 0){
			memory_values.push(index);
			memory_tile_ids.push(tile.id);

		} 

		else if(memory_values.length == 1){
			memory_values.push(index);
			memory_tile_ids.push(tile.id);

			if((memory_values[0].length > 20) && (memory_values[1].length < 20) && (memory_values[0] == gsi_dict[memory_values[1]])){
				console.log("go")

				tiles_flipped += 2;
				// Clear both arrays
				phrase = "You found "+ memory_values[1] +"!"
				alert(phrase)
				memory_values = [];
            	memory_tile_ids = [];

            	if(tiles_flipped == memory_array.length){
					alert("Great job naming those awesome GSI's. Get ready to play again!");
					document.getElementById('memory_board').innerHTML = "";
					newBoard();
				}
				
			}
			else if((memory_values[1].length > 20) && (memory_values[0].length < 20) && (memory_values[1] == gsi_dict[memory_values[0]])){
				console.log("go")
				tiles_flipped += 2;
				phrase = "You found "+memory_values[0] + "!"
				alert(phrase)
				// Clear both arrays
				memory_values = [];
            	memory_tile_ids = [];
            	if(tiles_flipped == memory_array.length){
					alert("Great job naming the CS61A staff. Get ready to play again!");
					document.getElementById('memory_board').innerHTML = "";
					newBoard();
				}
				
			}

			else {
				console.log("flip")
				function flip2Back(){
				    // Flip the 2 tiles back over
				    var tile_1 = document.getElementById(memory_tile_ids[0]);
				    var tile_2 = document.getElementById(memory_tile_ids[1]);
				    tile_1.style.background = '#CCC';
            	    tile_1.innerHTML = "";
				    tile_2.style.background = '#CCC';
            	    tile_2.innerHTML = "";
				    // Clear both arrays
				    memory_values = [];
            	    memory_tile_ids = [];
				}
				setTimeout(flip2Back, 700);
			}
		}
	}
}
</script>
</head>
<body>
<div id="memory_board"></div>
<script>newBoard();</script>
</body>
</html>
