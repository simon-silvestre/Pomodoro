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
              <input name="pomodoro" :value="pomodoroValue" type="number">
              <div class="selecteur">
                <img src="@/assets/up.svg" @click="pomodoro(1)" alt="ajouter">
                <img src="@/assets/down.svg" @click="pomodoro(-1)" alt="enlenver">
              </div>
            </div>
            <div class="input">
              <label for="shortbreak">short break</label>
              <input name="shortbreak" :value="shortbreakValue" type="number">
              <div class="selecteur">
                <img src="@/assets/up.svg" @click="shortBreak(1)" alt="ajouter">
                <img src="@/assets/down.svg" @click="shortBreak(-1)" alt="enlenver">
              </div>
            </div>
            <div class="input">
              <label for="longbreak">long break</label>
              <input name="longbreak" :value="longbreakValue" type="number">
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

        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  data() {
    return {
      pomodoroValue: 0,
      shortbreakValue: 0,
      longbreakValue: 0
    }
  },
  methods: {
    closeModal() {
      this.$parent.modal = false;
    },
    pomodoro(valeur) {
      if(valeur == -1 && this.pomodoroValue == 0 ){
        return
      }
      this.pomodoroValue += valeur
    },
    shortBreak(valeur) {
      if(valeur == -1 && this.shortbreakValue == 0 ){
        return
      }
      this.shortbreakValue += valeur
    },
    longBreak(valeur) {
      if(valeur == -1 && this.longbreakValue == 0 ){
        return
      }
      this.longbreakValue += valeur
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
    }
  }
}
</script>

<style scoped lang="scss">
  .container {
    position: fixed;
    left: 0px;
    top: 0px;
    background-color: rgba(0,0,0, 0.3);
    width: 100%;
    height: 100%;
    z-index: 100;
    color: #000;
  }
  .modal {
    width: 540px;
    height: 460px;
    background-color: #fff;
    border-radius: 25px;
    margin: 11% auto;
    
    .head, .inputContainer, .font, .color, .fontChoice {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
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
      border-bottom: 1px solid lightgray;
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
            top: 37px;
            right: 40px;

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
  }
  .font {
    .fontChoice {
      padding: 20px 0;
      & p {
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 40px;
        height: 40px;
        text-transform: capitalize;
        letter-spacing: 0;
        margin: 0 10px;
        background-color: #eef1fa;
        border-radius: 50%;

        &:nth-child(2) {
          font-family: 'Londrina Solid', cursive;
        }
        &:nth-child(3) {
          font-family: 'Roboto Slab', serif;
        }
      }
      .selectedFont {
        background-color: black;
        color: #fff;
      }
    }
  }
</style>
