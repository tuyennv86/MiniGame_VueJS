<template>
  <div id="app">
    <div class="wrapper clearfix">
      <players
        v-bind:scoresPlayer="scoresPlayer"
        v-bind:activePlay="activePlay"
        v-bind:currentPlayer="currentPlayer"
        v-bind:isWinner="isWinner"
      ></players>
      <controls
        v-on:handNewGame="actionNewGame"
        v-on:handRollDice="handRollDice"
        v-bind:isPlaying="isPlaying"
        v-on:handHold="handHold"
        v-bind:finalScore="finalScore"
        v-on:handChangFinalScore="handChangFinalScore"
      ></controls>
      <dices v-bind:dices="dices"></dices>
    </div>
    <popuprule
      v-bind:isOpenpopup="isOpenpopup"
      v-on:confirm="confirm"
    ></popuprule>
  </div>
</template>

<script>
import players from "./components/players";
import controls from "./components/controls";
import dices from "./components/dices.vue";
import popuprule from "./components/popuprule.vue";

export default {
  name: "app",
  data() {
    return {
      isPlaying: false,
      isOpenpopup: false,
      activePlay: 0, // neu bang 0 thi nguoi troi 1 bang 1 là nguoi choi 2
      scoresPlayer: [13, 30],
      currentPlayer: 10,
      dices: [2, 6],
      finalScore: 100,
    };
  },
  computed: {
    isWinner() {
      let { scoresPlayer, finalScore } = this;
      if (scoresPlayer[0] >= finalScore || scoresPlayer[1] >= finalScore) {
        this.isPlaying = false;
        return true;
      }
      return false;
    },
  },
  methods: {
    newPlayer() {
      this.activePlay = this.activePlay === 0 ? 1 : 0;
      this.currentPlayer = 0;
    },
    actionNewGame() {
      this.isOpenpopup = true;
      this.isPlaying = false;
    },
    handChangFinalScore(e) {
      let number = parseInt(e.target.value);
      if (isNaN(number)) {
        alert("Bạn phải nhập số !");
      } else {
        this.finalScore = number;
      }
    },
    handHold() {
      if (this.isPlaying) {
        // dang choi
        //activePlay = 0 ngoi choi 1 = 1 la nguoi choi 2
        //scoresPlayer la diem cua 2 nguoi choi dang choi

        let { scoresPlayer, activePlay, currentPlayer } = this;
        let scoreOld = scoresPlayer[activePlay];
        this.$set(this.scoresPlayer, activePlay, scoreOld + currentPlayer);
        if (!this.isWinner) {
          this.newPlayer();
        }
      } else {
        alert("Vui lòng nhấn nút NewGame");
      }
    },
    handRollDice() {
      if (this.isPlaying) {
        const a = Math.floor(Math.random() * 6) + 1;
        const b = Math.floor(Math.random() * 6) + 1;
        this.dices = [a, b];
        if (a === 1 || b === 1) {
          let paly = this.activePlay + 1;
          setTimeout(function () {
            alert(`Người chơi ${paly} đã quy trúng số 1. Rất tiếc...`);
          }, 10);

          this.newPlayer();
        } else {
          this.currentPlayer = this.currentPlayer + a + b;
        }
      } else {
        alert("Vui lòng nhất vào nut NewGame");
      }
    },
    confirm() {
      this.isOpenpopup = false;
      this.isPlaying = true;
      this.activePlay = 0;
      this.scoresPlayer = [0, 0];
      this.currentPlayer = 0;
      this.dices = [1, 1];
    },
  },
  components: {
    players,
    controls,
    dices,
    popuprule,
  },
};
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
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("/public/assets/back.jpg");
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
