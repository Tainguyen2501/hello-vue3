<template>
    <div class="wrapper-alert" :class="{'open-alert': isOpenAlert === true}">
  <div class="rule-alert">
    <h2> Please Press New Game</h2>
    <button
        @click="confirmAlert"
        class="confirm">Done</button>
    <button
        @click="openNewGame"
        class="confirm"> New game</button>
  </div>
    </div>
</template>

<script>
export default {
  name: "AlertRule",
  data(){
    return{

    }
  },
  props:{
    isOpenAlert:{
      type:Boolean,
      Default:false,
    }
  },
  methods:{
    confirmAlert(){
      // console.log('confirmAlert trong Alert.vue')
      this.$emit('handleConfirmAlert')
    },
    openNewGame(){
      // console.log('openNewGame trong Alert.vue')
      this.$emit('handleOpenNewGame')
    }
  }
}
</script>

<style scoped>
.wrapper-alert{
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background-color: rgba(0,0,0,0.2);
display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  visibility: hidden;
  transform: scale(1.2);
  transition: all 0.3s ease-in;
}
.wrapper-alert.open-alert{
  opacity: 1;
  visibility: visible;
  transform: scale(1);
}
.rule-alert{
  position: absolute;
  background-color: white;
  width: 400px;
  height: 100px;
  font-family:Helvetica, Arial, sans-serif;
}
.rule-alert h2{
  padding: 10px;
}
.rule-alert .confirm{
  cursor: pointer;
  margin-top: 10px;
  margin-right: 5px;
  background-color: #222222;
  color: white;
  width: 70px;
  height: 35px;
  border: 2px solid #222222;
  transition: all 0.3s ease-in;
  float: right;
}
.rule-alert .confirm:hover{
  background-color: white;
  color: #000;
}

</style>