<template>
  <div class="wrapper-popup" :class="getClassPopup">
 <div class="rule">
   <h2>Luật chơi</h2>
   <p>Mỗi người xoay theo lượt của mình.Nhấn HOLD để lấy điểm. Ai lớn hơn số điểm khiêu chiến sẽ thắng </p>
   <p> <strong>Lưu ý:</strong>  Người nào quay trúng số 1 sẽ bị mất lượt chơi và không được cộng điểm cho lần đó </p>

   <button class="confirm"
           @click="confirm"
   >Đã hiểu</button>
 </div>
  </div>
</template>

<script>
export default {
  name: "PopupRule",
  data() {
    return {

    }
  },
  props:{
    isOpenPopup:{
      type: Boolean,
      Default: false,
    }
  },
  computed:{
    getClassPopup(){
      return{
        'open-popup':this.isOpenPopup
      }
    }
  },
  methods:{
    confirm(){
          // console.log('confirm trong PopupRule.vue')
      this.$emit('handleConfirm')
    }
  }

}
</script>

<style scoped>
.wrapper-popup{
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background-color: rgba(0,0,0,0.2);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease-in;

}
.wrapper-popup.open-popup{
  opacity: 1;
  visibility: visible;
}
.open-popup .rule{
  transform: translate(-50%,-50%) scale(1);
}
.rule{
  position: absolute;
  width: 400px;
  background-color: white;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%) scale(1.2);
  padding: 15px;
  font-family: Helvetica, Arial, sans-serif;
  transition: all 0.3s ease-in;
  text-align: justify;
}
.rule h2{
    margin-bottom: 10px;

}
.rule .confirm{

  cursor: pointer;
  margin-top: 10px;
  background-color: #222222;
  color: white;
  width: 70px;
  height: 35px;
  border: 2px solid #222222;
  transition: all 0.3s ease-in;
  float: right;

}
.rule .confirm:hover{
  background-color: white;
  color: #222222;
}
</style>