<template>
<div class="wrapper-notification" :class="{'open-noti': isOpenNotification}">
  <div class="notification ">
    <h2>Bạn Đã quay trúng số 1. Rất Tiếc!</h2>
    <button class="confirm-noti"
            @click="confirmNoti"
    >Đã Hiểu</button>
  </div>


</div>
</template>

<script>
export default {
  name: "Notification",
  data(){
    return{

    }
  },
  props:{
    isOpenNotification:{
      type:Boolean,
      Default:false
    }
  },
  methods:{
    confirmNoti(){
      console.log('confirmNoti trong Notifi.vue')
      this.$emit('handleConfirmNoti')
    }
  }
}
</script>

<style scoped>
.wrapper-notification{
  position: fixed;
  background-color: rgba(0,0,0,0.2);
  color: black;
  top:0;
  right: 0;
  left: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: scale(1.2);
  transition: all 0.3s ease-in;
  opacity: 0;
  visibility: hidden;

}
.notification{
background-color: white;
  height: 130px;
  padding: 10px;
  font-family: Helvetica, Arial, sans-serif;
}
.wrapper-notification.open-noti{
  transform: scale(1);
  opacity: 1;
  visibility: visible;
}
.open-noti{

}
.notification h2{
  padding: 10px;
}
.confirm-noti{
background-color:black;
  color: white;
  height: 34px;
  width: 70px;
  border: 2px solid black;
  float: right;
  margin-top: 30px;
  cursor: pointer;
  transition: all 0.3s ease-in;
}
.confirm-noti:hover{
  background-color: white;
  color: black;
}
</style>