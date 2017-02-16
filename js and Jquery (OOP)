var SG = {
  btns: [{ color: ".green", active: "activeGreen" },
         { color: ".red", active: "activeRed" },
         { color: ".yellow", active: "activeYellow" },
         { color: ".blue", active: "activeBlue" }], 
  
  sounds: ["sound1", "sound2", "sound3", "sound4", "error", "victory"],
  
  randomSequence: [],
  playerSequence: [],
  count: 0,
  strict: false,
  game: false
};

SG.highlightBtn = function(id) {
  $(SG.btns[id].color).addClass(SG.btns[id].active);
      setTimeout(function(){ //wait some time and make background color as it was
      $(SG.btns[id].color).removeClass(SG.btns[id].active);
      }, 300);
}

SG.playSound = function(id) { 
  $("#" + SG.sounds[id])[0].play(); 
}

//here and down

SG.playSequence = function() {
  $(".square").css("pointer-events", "none"); //disable colored buttons
  $("#screen").text(SG.count < 10 ? "0" + SG.count : SG.count); //zeropad 
       var i = 0;
       var interval = setInterval(function() {
        SG.playSound(SG.randomSequence[i]);
        SG.highlightBtn(SG.randomSequence[i]); 
        i++;
        if (i >= SG.randomSequence.length) {
            clearInterval(interval);
            $(".square").css("pointer-events", "auto"); //enable colored buttons
        }
     }, 600);     
  
  SG.playerSequence = []; //clear player input  
}

SG.randomGenerator = function() {
    SG.count = SG.count + 1; // update current round    
    SG.randomSequence.push(Math.floor(Math.random() * 4));  
    SG.playSequence();
}

//===== MEDIATOR ====
SG.start = function() {
  if (SG.game === false) {
    SG.randomGenerator(); 
    SG.game = true;
  } else { //if pressed START when game is running
    SG.reset(); //just    
    SG.game = false;
  }
}

SG.strictHandler = function() {
  if (SG.strict === false) {
     $("#bulb").css("background-color", "#f30a0a"); //light on
     SG.strict = true;
  } else {
     $("#bulb").css("background-color", "#32050c");  //light off
     SG.strict = false;
  }
}

SG.reset = function() {
    SG.randomSequence = [];
    SG.playerSequence = [];
    SG.count = 0;
    SG.strict = false;
    SG.game = false;
    $("#screen").text("--");
}
  
SG.checkPlayerInput = function(id) {
  if(SG.game === true) { //only if was pressed Start     
     SG.playerSequence.push(parseInt(id, 10)); //string into number
     SG.highlightBtn(id);
    
  for (var i = 0; i < SG.playerSequence.length; i++) {
   if (SG.randomSequence[i] !== SG.playerSequence[i]) {
      $("#screen").text("!!");
      SG.playSound(4); // error sound
           setTimeout(function() {// wait 2 sec, then reset or repeat seqence
            if (SG.strict === true) {             
               SG.reset();                            
            }
            else {
               SG.playerSequence.pop(); //remove last wrong number           
               SG.playSequence();                 
            }
          }, 2000);  
    } else {
       SG.playSound(id); //if reached here, play good sound  
    }
   }
    if (SG.playerSequence.length === 20) {
       setTimeout(function() { //if player repeated right 20 times in a row
          $("#screen").text("WIN");
          SG.playSound(5);
          setTimeout(function(){ 
          SG.reset();
          }, 4000);
       }, 1000);  
     }
    
     else if (SG.randomSequence.length === SG.playerSequence.length) {
       setTimeout(function() { //wait 1sec then repeat sequence and add new btn
       SG.randomGenerator();
       }, 1000);  
     }
  } 
}
//===== MEDIATOR'S END ====

// ==== VIEW ====

$('div').on('click', function() {
  
  if ($(this).is(".start")) {
    SG.start();
  }
  
  if ($(this).is( ".strict" )) {
   SG.strictHandler();   
  }
  
  if ($(this).is(".green, .red, .yellow, .blue")) {
   SG.checkPlayerInput(event.target.id);
  }
});
