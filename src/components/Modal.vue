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
              <input name="pomodoro" type="number">
              <div class="selecteur">
                <img src="@/assets/up.svg" alt="ajouter">
                <img src="@/assets/down.svg" alt="enlenver">
              </div>
            </div>
            <div class="input">
              <label for="shortbreak">short break</label>
              <input name="shortbreak" type="number">
              <div class="selecteur">
                <img src="@/assets/up.svg" alt="ajouter">
                <img src="@/assets/down.svg" alt="enlenver">
              </div>
            </div>
            <div class="input">
              <label for="longbreak">long break</label>
              <input name="longbreak" type="number">
              <div class="selecteur">
                <img src="@/assets/up.svg" alt="ajouter">
                <img src="@/assets/down.svg" alt="enlenver">
              </div>
            </div>
          </div>
        </div>
        <div class="font">

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
  methods: {
    closeModal() {
      this.$parent.modal = false;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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

    .head, .inputContainer, .font, .color {
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

    .time {
      padding: 20px 0;
      border-bottom: 1px solid lightgray;
      p {
        font-size: 14px;
        text-transform: uppercase;
        font-weight: bold;
        letter-spacing: 5px;
      }
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
            cursor: pointer;
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
              width: 12px;
            }
          }
        }
      }
    }
  }
</style>
