<template>
  <div id="app">
    <div class="wrapper clearfix">
            
            <players-comp />
            
            <controls-comp />
            
            <dices-comp />
      </div>
  </div>
</template>

<script>

import PlayersComp from './components/PlayersComp';
import ControlsComp from './components/ControlsComp';
import DicesComp from './components/DicesComp';

export default {
  name: 'app',
  data () {
    return {
      
    }
  },
  components: {
    PlayersComp,
    ControlsComp,
    DicesComp
  },
  methods: {

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
