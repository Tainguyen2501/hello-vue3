<template>

  <!-- built files will be auto injected -->
  <!--
isPlaying: true
score -> Có 2 điểm chính thức hành cho 2 người chơi
currentStore
dice1 - dice2
Làm sao để nhận diện được ai là người đang chơi?? -> Chỉ có 2 người
    -> Tạo biến để lưu
    activePlayer: 1 -> Người thứ nhất đang chơi
    activePlayer: 2 -> Người thứ hai đang chơi
NewGame
    1. Show Popup
    2. Reset Data
    3. Xay dựng Popup
Roll Dice
    1. Random dư liệu 2 con xúc xắc
    2. Kiểm tra xem người dùng có xuay đúng con số 1 không?
        2.1. Nếu xoay trúng số 1 -> Đổi lượt chơi -> Reset điểm tạm thời
        2.2. Nếu xoay ok -> Cộng dồn vào điểm tạm thời cho người chơi đó.
Hold -> Lấy điểm
    1. So sánh xem điểm cuối cùng lớn hơn FinalScore???
    2. Chưa đủ điểm -> Cộng dồn 'ĐIỂM CHÍNH THỨC' => Đổi lượt chơi
 -->
      <div class="list-group-numbered"> hi Nma</div>
  <div class="wrapper clearfix">
    <Players  :isWinner="isWinner"
              :scoresPlayer="scoresPlayer"
             :activePlayer="activePlayer"
             :currentScore="currentScore">
    </Players>

    <controls
        :isPlaying="isPlaying"
        :finalScore="finalScore"
        @handleChangeFinalScore="handleChangeFinalScore"
        @handleNewGame="handleNewGameEvent"
        @handleRollDice="handleRollDice"
        @handleHoldScore="handleHoldScore"

    ></controls>
    <dices
        :dices="dices"
    ></dices>
    <PopupRule
        :isOpenPopup="isOpenPopup"
        @handleConfirm="handleConfirm"
    ></PopupRule>

  <AlertRule :isOpenAlert="isOpenAlert"
             @handleConfirmAlert="handleConfirmAlert"
             @handleOpenNewGame="handleOpenNewGame"
  ></AlertRule>
  <Notification :isOpenNotification="isOpenNotification"
                @handleConfirmNoti="handleConfirmNoti"

  ></Notification>
  </div>
</template>

<script>
import Players from './components/Players.vue'
import controls from "./components/controls.vue";
import Dices from "./components/Dices.vue";
import PopupRule from "./components/PopupRule.vue";
import AlertRule from "./components/AlertRule.vue";
import Notification from "./components/Notification.vue";

export default {
  name: 'App',
  components: {
    Players,
    controls,
    Dices,
    PopupRule,
    AlertRule,
    Notification,
  },
  data() {
    return {
      activePlayer: 0,  // Người chơi hiện tại
      scoresPlayer: [10, 10],
      currentScore: 0,
      isPlaying: false,
      isOpenPopup: false,
      dices: [2, 3],
      isOpenAlert: false,
      isOpenNotification: false,
      finalScore: 20,

    }
  },
  computed:{
    isWinner(e) {
      let{scoresPlayer,finalScore} = this
      if(scoresPlayer[0] >= finalScore || scoresPlayer[1] >= finalScore) {
        e.isPlaying = false
        return true
      }

      return false
    },
  },

  methods: {

    handleChangeFinalScore(e) {
      console.log('handleChangeFinalScore trong App.vue:')
      console.log(parseInt(e.target.value))
      let number = parseInt(e.target.value)
      if (isNaN(number)) {
        this.finalScore = ""
      } else {
        this.finalScore = number
      }
    },
    handleHoldScore() {
      // console.log('handleHoldScore trong App.vue')
      if (this.isPlaying) {
        //activePlayer = 0 ==> người chơi 1 , activePlayer = 1 ==> người chơi 2
        //scorePlayer[0] = scorePlayer[activePlayer]
        /* Cách 1 */
        this.scoresPlayer[this.activePlayer] = this.scoresPlayer[this.activePlayer] + this.currentScore
        if(!this.isWinner){
          this.nextPlayer()
        }

        /* Cách 2
           let {scoresPlayer, activePlayer, currentScore} = this
        let scoreOld = scoresPlayer[activePlayer]
        let cloneScorePlayer = [...scoresPlayer];
        cloneScorePlayer[activePlayer] = scoreOld + currentScore;
        this.scoresPlayer = cloneScorePlayer
        this.nextPlayer()*/
      } else {
        this.isOpenAlert = true
      }
    },
    nextPlayer() {
      // activePlayer = 0 -->1, nếu activePlayer = 1 -->0
      this.activePlayer = this.activePlayer === 0 ? 1 : 0
      this.currentScore = 0
    },
    handleRollDice() {
      // console.log('handleRollDice trong App.vue')
      if (this.isPlaying) {
        // Xoay xúc xắc
        var dice1 = Math.floor(Math.random() * 6 + 1);
        var dice2 = Math.floor(Math.random() * 6 + 1);
        console.log('xúc sắc 1:', dice1, 'xúc sắc 2:', dice2)
        this.dices = [dice1, dice2]
        if (dice1 === 1 || dice2 === 1) {
          //Đổi lượt chơi ,reset điểm tạm thời về 0
          this.isOpenNotification = true
          this.nextPlayer()
          /*   var activePlaying =this.activePlayer
          setTimeout(function () {
            alert(`Người chơi Player ${activePlaying + 1} đã quay trúng số 1. Rất tiếc!`)
          }, 100) */

        } else {
          // Cộng dồn điểm tạm thời cho người chơi
          this.currentScore = this.currentScore + dice1 + dice2
        }
      } else {
        this.isOpenAlert = true
      }
    },
    handleNewGameEvent() {
      // console.log('handleNewGameEvent trong App.vue')
      this.isOpenPopup = true;
    },
    handleConfirm() {
      // console.log('handleConfirm trong App.vue')
      this.isOpenPopup = false;
      this.activePlayer = 0;
      this.scoresPlayer = [0, 0];
      this.isPlaying = true;
      this.dices = [1, 1];
      this.currentScore = 0
    },
    handleConfirmAlert() {
      // console.log('handleConfirmAlert trong App.vue')
      this.isOpenAlert = false
    },
    handleOpenNewGame() {
      // console.log('handleOpenNewGame trong App.vue')
      this.isOpenAlert = false;
      this.isOpenPopup = true
    },
    handleConfirmNoti() {
      this.isOpenNotification = false
    },

  }
}
</script>

<style>

/**********************************************
*** GENERAL
**********************************************/

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
  background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('https://github.com/luutruonghailan/hoc-lap-trinh-online-zendvn/blob/master/khoa-hoc-lap-trinh-vuejs/02.Chuong02/DiceGame_html/back.jpg?raw=true');
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
