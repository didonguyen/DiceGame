<template>
  <div id="app">
    <div class="wrapper clearfix">
            
            <players-comp 
              v-bind:isWinner="isWinner"
              v-bind:playerscore="playerscore"
              v-bind:currentscore="currentscore"
              v-bind:isPlaying="isPlaying"
              v-bind:activePlayer="activePlayer"
              />
            
            <controls-comp 
              v-bind:isPlaying="isPlaying"
              v-on:clickNewgameEvent="handleclickEvent"
              v-on:clickRollDice="clickRollDice"
              v-on:clickHold="clickHold"
              v-bind:finalScore="finalScore"
              v-on:handleFinalScore="handleFinalScore"
            />
            
            <dices-comp v-bind:dices="dices"/>

            <popup-rule 
              v-bind:isOpenPopup="isOpenPopup"
              v-on:handleConfirm="handleConfirm"
            />
      </div>
  </div>
</template>

<script>

import PlayersComp from './components/PlayersComp';
import ControlsComp from './components/ControlsComp';
import DicesComp from './components/DicesComp';
import PopupRule from './components/PopupRule';
export default {
  name: 'app',
  data () {
    return {
      isPlaying: false,
      isOpenPopup: false,
      activePlayer: 0,
      playerscore: [0,0],
      dices: [1, 5],
      currentscore: 0,
      finalScore: 10

    }
  },
  components: {
    PlayersComp,
    ControlsComp,
    DicesComp,
    PopupRule
  },
  computed: {
    isWinner() {
      let { playerscore, finalScore } = this;
      console.log(playerscore[0], playerscore[1], finalScore );

      if(playerscore[0] >= finalScore || playerscore[1] >= finalScore ){
        
        this.isPlaying = false;
        return true;
      }
        return false;
      
    }
  },
  methods: {
    handleFinalScore(e) {
      var number = parseInt(e.target.value);
      if(isNaN(number)){
        this.finalScore = '';
      }
      else{
        this.finalScore = number;
      }
      
    },
    clickHold() {
      if(this.isPlaying){

        let { playerscore, activePlayer, currentscore } = this;
        let oldScore = playerscore[activePlayer];

        //this.playerscore[this.activePlayer] = this.playerscore[this.activePlayer] + this.currentscore;
        //this.playerscore[activePlayer] = oldScore + currentscore;
        this.$set(this.playerscore, activePlayer, oldScore + currentscore);

        if( !this.isWinner ){
          this.nextPlayer();
        }
        
      }
      else{
        alert('NewGame Please!');
      }
    },
    nextPlayer(){
      this.activePlayer = this.activePlayer ==0? 1 : 0;
      this.currentscore = 0;
    },
    handleclickEvent(){
      this.isOpenPopup = true;
    },
    handleConfirm(){
      this.isPlaying = true;
      this.isOpenPopup = false;
      this.activePlayer = 0;
      this.playerscore = [0, 0];
      this.currentscore = 0;
      this.dices = [1, 1];
    },
    clickRollDice(){
      if(this.isPlaying == false){
        alert('NewGame Please!');
        
      }
      else{
        var dice1 = Math.floor(Math.random() * 6) + 1;
        var dice2 = Math.floor(Math.random() * 6) + 1;
        this.dices = [dice1,dice2];
        if(dice1 === 1 || dice2 === 1){
          setTimeout(() => {
            alert(`Sorry, You Player ${this.activePlayer + 1} lost yourturn`);
            this.nextPlayer();
          }, 10)
          
          
          
        }
        else{
          this.currentscore = this.currentscore + dice1 + dice2;
        }
      }
    }
  }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url(/public/assets/back.jpg);
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}
</style>
