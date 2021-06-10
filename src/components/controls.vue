<template>
<div class="wrapper-control">
  <button
      @click="newGame"
      class="control btn-new"><i class="ion-ios-plus-outline"></i>New game</button>
  <button
      @click="rollDice"
      class="control btn-roll"><i class="ion-ios-loop"></i>Roll dice</button>
  <button
      @click="$emit('handleHoldScore')"
      class="control btn-hold"><i class="ion-ios-download-outline"></i>Hold</button>

<!-- Cách 1:  <input
      :value="valueDemo"
      @input="valueDemo =$event.target.value"
      type="number" placeholder="Final score" class="final-score">-->

<!-- Cách 2:  <input
      :value="valueDemo"
      @input="handleDemo"
      type="number" placeholder="Final score" class="final-score">  -->

  <!-- cách 1
    <input
      :value="finalScore"
     @input="ChangeFinalScore"
    type="number" placeholder="Final score" class="final-score">-->

  <input
      :disabled="isPlaying"
      :value="finalScore"
      @input="$emit('handleChangeFinalScore',$event)"
      type="number" placeholder="Final score" class="final-score">
</div>
</template>

<script>
export default {
  name: "controls",
  data(){
    return{
        valueDemo: 100,
    }
  },
  props:{
    finalScore:{
      type:[Number,String],
      Default:100,
    },
    isPlaying:{
      type: Boolean,
      Default: false,
    }
  },
  methods:{
    /* ChangeFinalScore(){
      this.$emit('handleChangeFinalScore',event)
    }, */

    /*  handleDemo(e){
      console.log(e.target.value)
      this.valueDemo = e.target.value
    }, */

    newGame(){
        // console.log('NewGame trong Controls.vue',this)
      this.$emit('handleNewGame')
    },
    rollDice(){
      // console.log('rollDice trong ConTrols.vue')
      this.$emit('handleRollDice')
    }
  },
}


</script>

<style scoped>
/**********************************************
*** Control
**********************************************/
.control {
  position: absolute;
  width: 200px;
  left: 50%;
  transform: translateX(-50%);
  color: #555;
  background: none;
  border: none;
  font-family: Lato;
  font-size: 20px;
  text-transform: uppercase;
  cursor: pointer;
  font-weight: 300;
  transition: background-color 0.3s, color 0.3s;
}

.control.disable {
  pointer-events: none;
}

.control:hover {
  font-weight: 600;
}

.control:hover i {
  margin-right: 20px;
}

.control:focus {
  outline: none;
}

.control i {
  color: #42b983;
  display: inline-block;
  margin-right: 15px;
  font-size: 32px;
  line-height: 1;
  vertical-align: text-top;
  margin-top: -4px;
  transition: margin 0.3s;
}

.btn-new {
  top: 45px;
}

.btn-roll {
  top: 403px;
}

.btn-hold {
  top: 467px;
}

.final-score {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 520px;
  color: #555;
  font-size: 18px;
  font-family: 'Lato';
  text-align: center;
  padding: 10px;
  width: 160px;
  text-transform: uppercase;
}

.final-score:focus {
  outline: none;
}
</style>