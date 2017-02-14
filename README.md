# Simon-Game

>Simon Game is a simple game which goal is for user to repeat the pattern showed by the program. With each round a new step is added to the pattern making, the game much more difficult with every round. Additionally, the program should play a different sound for each field that is activated. On top Of that you have to enable user to switch between strict mode, which restarts a game whenever user selects wrong field in a pattern, and normal mode which only repeats the pattern subsequent of the wrong button being pressed. The provided example constituted of 4 different fields with different color for each field and I followed with the same idea.

Watch short video about 
[How to play Simon Game](https://www.youtube.com/watch?v=1Yqj76Q4jJ4)

My html code is pretty plain. Many ```div``` and ```audio``` tags. Audio preloading before it needs to be executed.

CSS a little bit trickier. I spent the whole evening on a layout of my game, trying to find right colors and shadows.  ```border-radius``` let me have round buttons and smooth corners. Also, I wildly used ```box-shadow``` to make buttons look more real. And remove ```box-shadow``` on START and STRICT buttons to imitate click. 

CSS3 have *animation* and *transition*.  But I think for this project it would be redundant  

##HTML

```html
<head>
  <audio id="sound1" src="https://s3.amazonaws.com/freecodecamp/simonSound1.mp3" preload="auto"></audio>
  <audio id="sound2" src="https://s3.amazonaws.com/freecodecamp/simonSound2.mp3" preload="auto"></audio>
  <audio id="sound3" src="https://s3.amazonaws.com/freecodecamp/simonSound3.mp3" preload="auto"></audio>
  <audio id="sound4" src="https://s3.amazonaws.com/freecodecamp/simonSound4.mp3" preload="auto"></audio>
  <audio id="error" src="https://ia800209.us.archive.org/1/items/simo_game_audio/error.mp3" preload="auto"></audio>
  <audio id="victory" src="https://ia600209.us.archive.org/1/items/simo_game_audio/victory.mp3" preload="auto"></audio>
</head>

<div id="game"> 
    
<div id="circle">
  
  <h1>Simon</h1>   
  
  <div class="control">
    <div class="btn start"></div>
    <h3>START</h3>
  </div>
  
  <div id="bulb"></div>
  
  <div class="control">    
    <div class="btn strict"></div>
    <h3>STRICT</h3>
  </div>   
    
  <div id="screen">--</div>
  <h3>COUNT</h3>
  
</div>    
  
    <div class="square green" id="0"></div>
    <div class="square red" id="1"></div>
    <div class="square yellow" id="2"></div>
    <div class="square blue" id="3"></div>  
  
</div>

```
===

##CSS

```css

body {  
  background: url('http://wallpapercave.com/wp/zwaIWUh.jpg') no-repeat;
  background-color: #314359;
  user-select: none;
  color: #314359;
}

#game {
  width: 550px;
  height: 550px;
  margin: 10vh auto;
  position: relative;
}

 #circle {
  width: 265px;  
  height: 265px;
  position: absolute;
  left: 23%;
  top: 23%;
  z-index: 100;
  box-shadow: 0px 0px 55px #000;
  background-color: #b6b6b6;
  border: 15px solid #ece7ee;
  border-radius: 50%;
  }

h1 {
  margin-top: 25px;
  text-align: center;
  font: 60px 'Lobster', cursive;
}

.control {
  display: inline-block;  
  margin-top: -60px;
  height: 60px;
  width: 60px;
}

.control:nth-child(2){  
  margin: -20px 20px 20px 65px;
}

.btn { 
  margin: 0px 12.7px 0px 12.7px;
  width: 30px;  
  height: 30px;
  border-radius: 50%;
  border: 2px solid #272725; 
  cursor: pointer;
  background: #ffff00;
  box-shadow: 0px 2px 6px #000;
}

.btn:active {
  box-shadow: 0px 0px 0px #000;
}
.start {
  background: #ff0000;
}

h3 {
  margin-top: 5px;
  font: 11px 'Oswald';
  text-align: center; 
}

#bulb {
  position: absolute;
  left: 189px;
  top: 107px;
  width: 8px;  
  height: 8px;
  background: #32050c;
  border: 2px solid #272725; 
  border-radius: 50%;    
}

#screen {
  width: 65px;  
  height: 35px;
  background: #1d1d1d;
  border: 2px solid #ece7ee;
  border-radius: 5px;
  margin: -9px auto 0px;
  text-align: center;  
  font: 35px 'VT323', cursive;
  color: #f08b48;
}

.square {    
  float: left;
  width: 245px;  
  height: 245px;  
  border: 5px solid #ece7ee;
  margin: 10px;
  box-shadow:
		inset 0 0 3px 1px rgba(0,0,0,.8),
		inset rgba(0,0,0,.3) -5px -5px 8px 5px,
		inset rgba(255,255,255,.5) 5px 5px 8px 5px,
		1px 1px 1px rgba(255,255,255,.1),
		-2px -2px 5px rgba(0,0,0,.5);
}

.green {
  background: linear-gradient(to bottom right, green, #00FF00);
  border-radius: 100% 5% 0 5%;
}

.activeGreen {
  background: #00e600;
  	box-shadow:
		inset 0 0 5px 3px rgba(0,0,0,.8),
		inset rgba(0,0,0,.3) -5px -5px 8px 5px,
		inset rgba(255,255,255,.5) 5px 5px 8px 5px,
		1px 1px 1px rgba(255,255,255,.2),
		-2px -2px 5px rgba(0,0,0,.5);
}

.red {
  background: linear-gradient(to bottom left, red, #e60000);
  border-radius: 5% 100% 5% 0;  
}

.activeRed {
  background: #FF7979;
  	box-shadow:
		inset 0 0 5px 3px rgba(0,0,0,.8),
		inset rgba(0,0,0,.3) -5px -5px 8px 5px,
		inset rgba(255,255,255,.5) 5px 5px 8px 5px,
		1px 1px 1px rgba(255,255,255,.2),
		-2px -2px 5px rgba(0,0,0,.5);
}

.yellow {
  background: linear-gradient(to top right, yellow, rgb(255, 255, 10));
  border-radius: 5% 0 5% 100%;  
}

.activeYellow {
  background: #FFFF95;
  	box-shadow:
		inset 0 0 5px 3px rgba(0,0,0,.8),
		inset rgba(0,0,0,.3) -5px -5px 8px 5px,
		inset rgba(255,255,255,.5) 5px 5px 8px 5px,
		1px 1px 1px rgba(255,255,255,.2),
		-2px -2px 5px rgba(0,0,0,.5);
}

.blue {
  background: linear-gradient(to top left, blue, #A6A6FF);
  border-radius: 0 5% 100% 5%;
}

.activeBlue {
  background: #0096ff;
  	box-shadow:
		inset 0 0 5px 3px rgba(0,0,0,.8),
		inset rgba(0,0,0,.3) -5px -5px 8px 5px,
		inset rgba(255,255,255,.5) 5px 5px 8px 5px,
		1px 1px 1px rgba(255,255,255,.2),
		-2px -2px 5px rgba(0,0,0,.5);
}

```
##Javasript

Here is an example of *Functional JavaScript Programming*. I implemented *JavaScript Design Patterns* **Model-View-Controller (MVC)** for keeping particular pieces of code independent of other components. MVC have different names, but the same meaning. To provide loose coupling to support well-structured code. In this version of Simon game, I created Object constructor, some global variables, and functions. And added an event listener to my buttons. Thanks to Jquery. I like handy way manipulation with DOM, animation and others features. My code is pretty self-explanatory. So I won't describing in detail what it does. 

===
Model

```javasript
function MakeButton(btn, cls) {
  this.btn = btn; 
  this.cls = cls;
}

var btns = [new MakeButton(".green", "activeGreen"),
            new MakeButton(".red", "activeRed"),
            new MakeButton(".yellow", "activeYellow"),
            new MakeButton(".blue", "activeBlue")];

var sounds = ["sound1", "sound2", "sound3", "sound4", "error", "victory"];

var randomSequence = [],
    playerSequence = [],
    count = 0,
    strict = false,
    game = false;

function highlightBtn(id) {
  $(btns[id].btn).addClass(btns[id].cls);
      setTimeout(function(){ //wait some time and make background color as it was
      $(btns[id].btn).removeClass(btns[id].cls);
      }, 300);
}

function playSound(id) { 
  $("#" + sounds[id])[0].play(); 
}

function playSequence() {
  $(".square").css("pointer-events", "none"); //disable colored buttons
  $("#screen").text(count < 10 ? "0" + count : count); //add zero when necessary  
       var i = 0;
       var interval = setInterval(function() {
        playSound(randomSequence[i]);
        highlightBtn(randomSequence[i]); 
        i++;
        if (i >= randomSequence.length) {
            clearInterval(interval);
            $(".square").css("pointer-events", "auto"); //enable colored buttons
        }
     }, 600);     
  
  playerSequence = []; //clear player input  
}

function randomGenerator() {
    count++; // update current round    
    randomSequence.push(Math.floor(Math.random() * 4));  
    playSequence();
}
```
===
Controller or Octopus

```javasript

function start() {
  game = game === false ? true : false;
  if (game) {
    randomGenerator(); 
  } else { //if pressed START when game is running
    reset(); //just    
  }
}

function strictHandler() {
  strict = strict === true ? false : true; 
  if (strict) {
     $("#bulb").css("background-color", "#f30a0a"); //light on
  } else {
     $("#bulb").css("background-color", "#32050c");  //light off
  }
}

function reset() {
    randomSequence = [];
    playerSequence = [];
    count = 0;
    strict = false;
    game = false;
    $("#screen").text("--");
}
  
function checkPlayerInput(id) {
  if(game) { //only if was pressed Start     
     playerSequence.push(parseInt(id, 10)); //string into number
     highlightBtn(id);
    
  for (var i = 0; i < playerSequence.length; i++) {
   if (randomSequence[i] !== playerSequence[i]) {
      $("#screen").text("!!");
      playSound(4); // error sound
           setTimeout(function() {// wait 2 sec, then reset or repeat seqence
            if (strict) {             
               reset();                            
            }
            else {
               playerSequence.pop(); //remove last wrong number           
               playSequence();                 
            }
          }, 2000);  
    } else {
       playSound(id); //if reached here, play good sound  
    }
   }
    if (playerSequence.length === 20) {
       setTimeout(function() { //if player repeated right 20 times in a row
          $("#screen").text("WIN");
          playSound(5);
          setTimeout(function(){ 
          reset();
          }, 4000);
       }, 1000);  
     }
    
     else if (randomSequence.length === playerSequence.length) {
       setTimeout(function() { //wait 1sec then repeat sequence and add new btn
       randomGenerator();
       }, 1000);  
     }
  } 
}

```

====
View

```javasript

$('div').on('click', function() {
  
  if ($(this).is(".start")) {
    start();
  }
  
  if ($(this).is( ".strict" )) {
   strictHandler();   
  }
  
  if ($(this).is(".green, .red, .yellow, .blue")) {
     checkPlayerInput(event.target.id);
  }
}); 

```

 Global variables are a weak spot of JavaScript. It can be easily avoidable with *Immediately-Invoked-Function-Expressions (IIFE)* to allow for private scopes to protect variables and methods. I didn't do this. 
