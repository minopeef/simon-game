// ==== MODEL ====
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
}//.get(0).cloneNode().play();

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

//===== MEDIATOR ====
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
//===== MEDIATOR'S END ====

// ==== VIEW ====

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
