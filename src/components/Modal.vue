<template>
  <div class="container">
    <div class="modal">
      <div class="head">
        <p>Settings</p>
        <span @click="closeModal()">X</span>
      </div>
      <div class="center">
        <div class="time">
          <p>time (minutes)</p>
          <div class="inputContainer">
            <div class="input">
              <label for="pomodoro">pomodoro</label>
              <input name="pomodoro" :value="$parent.pomodoroValue" type="number">
              <div class="selecteur">
                <img src="@/assets/up.svg" @click="pomodoro(1)" alt="ajouter">
                <img src="@/assets/down.svg" @click="pomodoro(-1)" alt="enlenver">
              </div>
            </div>
            <div class="input">
              <label for="shortbreak">short break</label>
              <input name="shortbreak" :value="$parent.shortbreakValue" type="number">
              <div class="selecteur">
                <img src="@/assets/up.svg" @click="shortBreak(1)" alt="ajouter">
                <img src="@/assets/down.svg" @click="shortBreak(-1)" alt="enlenver">
              </div>
            </div>
            <div class="input">
              <label for="longbreak">long break</label>
              <input name="longbreak" :value="$parent.longbreakValue" type="number">
              <div class="selecteur">
                <img src="@/assets/up.svg" @click="longBreak(1)" alt="ajouter">
                <img src="@/assets/down.svg" @click="longBreak(-1)" alt="enlenver">
              </div>
            </div>
          </div>
        </div>
        <div class="font">
          <p>Font</p>
          <div class="fontChoice">
            <p :class="{ selectedFont : $parent.poppins }" @click="fontChoice(1)">Aa</p>
            <p :class="{ selectedFont : $parent.oswald }" @click="fontChoice(2)">Aa</p>
            <p :class="{ selectedFont : $parent.roboto }" @click="fontChoice(3)">Aa</p>
          </div>
        </div>
        <div class="color">
          <p>Color</p>
          <div class="colorChoice">
            <span @click="colorChoice(1)"><img v-show="$parent.saumon" src="@/assets/check.svg" alt="check"></span>
            <span @click="colorChoice(2)"><img v-show="$parent.bleu" src="@/assets/check.svg" alt="check"></span>
            <span @click="colorChoice(3)"><img v-show="$parent.violet" src="@/assets/check.svg" alt="check"></span>
          </div>
        </div>
        <button @click.prevent="confirmModal()">Apply</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  methods: {
    closeModal() {
      this.$parent.modal = false;
      this.$parent.poppins = true
      this.$parent.oswald = false
      this.$parent.roboto = false
      this.$parent.saumon = true
      this.$parent.bleu = false
      this.$parent.violet = false
      this.$parent.pomodoroValue = 0
      this.$parent.shortbreakValue = 0
      this.$parent.longbreakValue = 0
    },
    confirmModal() {
      this.$parent.modal = false;
    },
    pomodoro(valeur) {
      if(valeur == -1 && this.$parent.pomodoroValue == 0 ){
        return
      }
      this.$parent.pomodoroValue += valeur
    },
    shortBreak(valeur) {
      if(valeur == -1 && this.$parent.shortbreakValue == 0 ){
        return
      }
      this.$parent.shortbreakValue += valeur
    },
    longBreak(valeur) {
      if(valeur == -1 && this.$parent.longbreakValue == 0 ){
        return
      }
      this.$parent.longbreakValue += valeur
    },
    fontChoice(item) {
      this.$parent.poppins = false
      this.$parent.oswald = false
      this.$parent.roboto = false
      if(item == 1) {
        this.$parent.poppins = true
      }
      else if(item == 2) {
        this.$parent.oswald = true
      }
      else if(item == 3) {
        this.$parent.roboto = true
      }
    },
    colorChoice(item) {
      this.$parent.saumon = false
      this.$parent.bleu = false
      this.$parent.violet = false
      if(item == 1) {
        this.$parent.saumon = true
      }
      else if(item == 2) {
        this.$parent.bleu = true
      }
      else if(item == 3) {
        this.$parent.violet = true
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .head, .inputContainer, .font, .color, .fontChoice, .colorChoice, .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .container {
    position: fixed;
    left: 0px;
    top: 0px;
    background-color: rgba(0,0,0, 0.3);
    width: 100%;
    height: 100%;
    z-index: 100;
    color: #000;
    justify-content: center;
  }
  .modal {
    max-width: 540px;
    height: 460px;
    background-color: #fff;
    border-radius: 25px;

    .head {
      padding: 40px 40px 25px 40px;
      font-weight: 900;
      font-size: 30px;
      border-bottom: 1px solid lightgrey;

      span {
        cursor: pointer;
        color: grey;
        font-size: 18px;
      }
    }
  }
  .center {
    padding: 0 40px;

    p {
        font-size: 14px;
        text-transform: uppercase;
        font-weight: 900;
        letter-spacing: 5px;
      }
    .time {
      padding: 20px 0;
      .inputContainer {
        padding: 20px 0 0 0;

        label {
          font-size: 12px;
          color: #afafaf;
          font-weight: 900;
        }
        .input {
          position: relative;

          input {
            width: 130px;
            height: 45px;
            background-color: #eef1fa;
            border: none;
            border-radius: 10px;
            margin-top: 5px;
            padding: 15px;
            font-weight: 900;
            outline-color: #1f2140;
            -webkit-appearance: textfield;
            -moz-appearance: textfield;
            appearance: textfield;

            &::-webkit-inner-spin-button, &::-webkit-outer-spin-button {
              appearance: none;
            }
          }
          .selecteur {
            display: grid;
            position: absolute;
            width: 10px;
            height: 10px;
            top: 53%;
            left: 100px;

            img {
              cursor: pointer;
              width: 12px;
              transition: ease 0.3s;

              &:hover {
                width: 15px;
              }
            }
          }
        }
      }
    }
    button {
      position: relative;
      width: 140px;
      height: 50px;
      border-radius: 50px;
      background-color: #f86f6b;
      color: #fff;
      border: none;
      margin: 0 auto;
      cursor: pointer;
      transition: ease 0.3s;
      font-weight: 900;
      font-size: 14px;
      left: calc(50% - 70px);

      &:active {
        transform: scale(1.03);
        outline: none;
      }
    }
  }
  .fontChoice {
    padding: 20px 0;
    p {
      text-transform: capitalize;
      letter-spacing: 0;
      background-color: #eef1fa;

      &:nth-child(1) {
        font-family: 'Poppins', sans-serif!important;
      }
      &:nth-child(2) {
        font-family: 'Open Sans', sans-serif!important;
      }
      &:nth-child(3) {
        font-family: 'Roboto Slab', serif!important;
      }
    }
    .selectedFont {
      background-color: black;
      color: #fff;
    }
  }
  .fontChoice p, .colorChoice span {
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin: 0 10px;
  } 

  .colorChoice {
    padding: 20px 0;

    span {
      &:nth-child(1) {
        background-color: #f86f6b;
      }
      &:nth-child(2) {
        background-color: #70f3f7;
      }
      &:nth-child(3) {
        background-color: #da81f4;
      }

      img {
        width: 15px;
      }
    }
  }
  .time, .font {
    border-bottom: 1px solid lightgray;
  }
</style>
