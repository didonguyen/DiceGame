<template>
  <div class="wrapper-popup" v-bind:class="getClassPopup">
      <div class="rule">
          <h3>Game's Rule</h3>
          <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Consequuntur dolorum sed dolores tempora quaerat voluptatum earum veritatis quibusdam fuga cumque voluptatibus soluta rem accusamus autem, optio ipsam provident iste nulla?</p>
          <button class="confirm" v-on:click="handleClickGotIt">Got it</button>
      </div>
  </div>
</template>

<script>
export default {
  name: 'PopupRule',
  props: {
      isOpenPopup: { type: Boolean,  default: false}
  },
  data() {
      return {
          
      }
  },
  computed: {
      getClassPopup: function(){
          return {
              'open-popup': this.isOpenPopup
          }
      }
  },
  methods: {
      handleClickGotIt(){
          
      }
  }
};
</script>

<style>
.wrapper-popup{
    position: fixed;
    background-color: rgba(0, 0, 0, 0.4);
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    opacity: 0;
    visibility: hidden;
    transition: all .3s ease;
}
.wrapper-popup.open-popup{
    opacity: 1;
    visibility: visible;
}
.rule{
    width: 350px;
    padding: 30px;
    background-color: #fff;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(1.2);
    font-family: Arial, Helvetica, sans-serif;
    transition: all .3s ease;
}
.open-popup .rule{
    transform: translate(-50%, -50%) scale(1);
}

.rule h3{
    margin-bottom: 10px;
}
.rule .confirm{
    margin-top: 10px;
    padding: 5px 10px;
    background-color: rgb(69, 70, 70);
    color: #fff;
    transition: all .3s ease;
}
.rule .confirm:hover{
    cursor: pointer;
    background-color: #fff;
    color: #333;
}
</style>
