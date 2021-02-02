<template>
  <div id="app" :class="{ oswald : oswald, roboto : roboto }">
    <Modal v-if="modal" />
    <h1>pomodoro</h1>
    <div class="navbar">
      <span class="navbar_item" :class="{ navbar_item__selected : pomodoro, saumon : saumon, bleu : bleu, violet : violet  }" @click="navbarChoice(1)">pomodoro</span>
      <span class="navbar_item" :class="{ navbar_item__selected : shortBreak, saumon : saumon, bleu : bleu, violet : violet  }" @click="navbarChoice(2)">short break</span>
      <span class="navbar_item" :class="{ navbar_item__selected : longBreak, saumon : saumon, bleu : bleu, violet : violet  }" @click="navbarChoice(3)">long break</span>
    </div>
    <div class="compteur" @click="timer()">
      <vue-ellipse-progress :progress="pause ? 100: progress" :color="choixCouleur()" emptyColor="transparent" :thickness="10" :size="mobileView ? 250 : 350">
        <div class="compteur_informations">
          <div class="compteur_temps">
            <p v-show="pomodoro">{{ pomodoroValue == pomodoroTotal / 60 ? pomodoroValue >= 10 ? pomodoroValue : '0' + pomodoroValue : minutes >= 10 ? minutes : '0' + minutes }}:{{ pomodoroValue == pomodoroTotal / 60 ?  '00' : secondes >= 10 ? secondes : '0' + secondes }}</p>
            <p v-show="shortBreak">{{ shortbreakValue == shortbreakTotal / 60 ? shortbreakValue : minutes }}:{{ shortbreakValue == shortbreakTotal / 60 ? 0 :secondes }}</p>
            <p v-show="longBreak">{{ longbreakValue == longbreakTotal / 60 ? longbreakValue : minutes }}:{{ longbreakValue == longbreakTotal / 60 ? 0 :secondes }}</p>
          </div>
          <div class="compteur_etat">
            <p v-if="pause">pause</p>
            <p v-else>play</p>
          </div>
        </div>
      </vue-ellipse-progress>
    </div>
    <img class="settings" src="@/assets/gear.svg" alt="parametres" @click="modal = !modal, stop()">
  </div>
</template>

<script>
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    Modal
  },
  data() {
    return {
      pomodoro: true,
      shortBreak: false,
      longBreak: false,
      pomodoroValue: 0,
      shortbreakValue: 0,
      longbreakValue: 0,
      pomodoroTotal: 0,
      shortbreakTotal: 0,
      longbreakTotal: 0,
      progress: 100,
      modal: false,
      poppins: true,
      oswald: false,
      roboto: false,
      saumon: true,
      bleu: false,
      violet: false,
      pause: true,
      pomodoroInterval: null,
      shortbreakInterval: null,
      longbreakInterval: null,
      minutes: 0,
      secondes: 0,
      mobileView: false,
    }
  },
  methods: {
    handleView() {
      this.mobileView = window.innerWidth <= 500;
    },
    stop() {
      this.pomodoroTotal = this.pomodoroValue * 60
      this.shortbreakTotal = this.shortbreakValue * 60
      this.longbreakTotal = this.longbreakValue * 60
      clearInterval(this.pomodoroInterval)
      clearInterval(this.shortbreakInterval)
      clearInterval(this.longbreakInterval)
      this.pause = true
    },
    navbarChoice(item) {
      this.pomodoro = false
      this.shortBreak = false
      this.longBreak = false
      this.stop();
      if(item == 1) {
        this.pomodoro = true
      }
      else if(item == 2) {
        this.shortBreak = true
      }
      else if(item == 3) {
        this.longBreak = true
      }
    },
    choixCouleur() {
      if(this.saumon == true) {
        return "#f86f6b"
      }
      if(this.bleu == true) {
        return "#70f3f7"
      }
      if(this.violet == true) {
        return "#da81f4"
      }
    },
    timer() {
      if(this.pause == false) {
        clearInterval(this.pomodoroInterval)
        clearInterval(this.shortbreakInterval)
        clearInterval(this.longbreakInterval)
        this.pause = true
      }
      else if(this.pause == true) {
        if(this.pomodoro == true && this.pomodoroValue * 60 > 0) {
        this.pause = !this.pause
        this.pomodoroInterval = setInterval(() => { 
          if(this.pomodoroTotal > 0) {
            this.minutes = Math.floor(this.pomodoroTotal / 60)
            this.secondes = Math.floor(this.pomodoroTotal % 60)
            this.pomodoroTotal--
            this.progress = this.pomodoroTotal * 100 / (this.pomodoroValue * 60)
          }
          else {
            clearInterval(this.pomodoroInterval)
            this.pause = true
            this.minutes = this.pomodoroValue
            this.secondes = 0
            this.pomodoroTotal = this.pomodoroValue * 60
            this.progress = 100
          }
         }, 1000)
        }
        else if(this.shortBreak == true && this.shortbreakValue * 60 > 0 ) {
          this.pause = !this.pause
          this.shortbreakInterval = setInterval(() => { 
            if(this.shortbreakTotal > 0) {
              this.minutes = Math.floor(this.shortbreakTotal / 60)
              this.secondes = Math.floor(this.shortbreakTotal % 60)
              this.shortbreakTotal--
              this.progress = this.shortbreakTotal * 100 / (this.shortbreakValue * 60)
          }
            else {
              clearInterval(this.shortbreakInterval)
              this.pause = true
              this.minutes = this.shortbreakValue
              this.secondes = 0
              this.shortbreakTotal = this.shortbreakValue * 60
              this.progress = 100
            }
          }, 1000)
        }
        else if(this.longBreak == true && this.longbreakValue * 60 > 0) {
          this.pause = !this.pause
          this.longbreakInterval = setInterval(() => { 
            if(this.longbreakTotal > 0) {
              this.minutes = Math.floor(this.longbreakTotal / 60)
              this.secondes = Math.floor(this.longbreakTotal % 60)
              this.longbreakTotal--
              this.progress = this.longbreakTotal * 100 / (this.longbreakValue * 60)
          }
            else {
              clearInterval(this.longbreakInterval)
              this.pause = true
              this.minutes = this.longbreakValue
              this.secondes = 0
              this.longbreakTotal = this.longbreakValue * 60
              this.progress = 100
            }
          }, 1000)
        }
      }
    }
  },
  created() {
    this.handleView();
      window.addEventListener('resize', this.handleView);
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto+Slab:wght@700&display=swap');
  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  body {
    background-color: #1f2140;
    color: #dae1fd;
  }
  #app {
    font-family: 'Poppins', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  #app.oswald {
    font-family: 'Open Sans', sans-serif;
  }
  #app.roboto {
    font-family: 'Roboto Slab', serif;
  }
  h1 {
    width: fit-content;
    margin: 50px auto;
  }
  .navbar, .compteur {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .navbar {
    width: 375px;
    height: 60px;
    margin: 0 auto;
    font-size: 13px;
    font-weight: 900;
    background-color: #161a32;
    color: #5d617b;
    border-radius: 100px;

    .navbar_item {
      padding: 14px 24px;
      cursor: pointer;
    }
    .navbar_item__selected {
      color: #4d212e;
      border-radius: 50px;
      transition: ease 0.5s;
    }
    .navbar_item__selected.saumon {
    background-color: #f86f6b;
    }
    .navbar_item__selected.bleu {
      background-color: #70f3f7;
    }
    .navbar_item__selected.violet {
      background-color: #da81f4;
    }
  }
  .compteur {
    margin: 40px auto;
    width: 410px;
    height: 410px;
    background-color: #161a32;
    border-radius: 50%;
    border: 20px solid #282b4f;
    box-shadow: 0px 0px 75px 0px #0f111d;
    cursor: pointer;
    transition: ease 0.2s;

    &:active {
      transform: scale(1.03);
    }
    .compteur_informations {
      top: -10px;
      position: relative;
    }
    .compteur_temps {
      font-size: 90px;
      font-weight: 900;
    }
    .compteur_etat {
      position: relative;
      top: 10px;
      font-weight: 900;
      text-transform: uppercase;
      letter-spacing: 15px;
    }
  }
  .settings {
    position: relative;
    width: 30px;
    top: 20px;
    left: calc(50% - 15px);
    cursor: pointer;
    padding-bottom: 50px;
  }

  @media screen and (max-width: 500px) {
    .navbar {
      width: 300px;
      font-size: 9px;

        .navbar_item {
          padding: 14px 22px;
        }
    }
    .compteur {
      width: 300px;
      height: 300px;
      border: 15px solid #282b4f;

      .compteur_temps {
        font-size: 70px;
        font-weight: 900;
      }
      .compteur_etat {
        font-size: 14px;
      }
    }
    circle.ep-circle--progress.animation__default {
    stroke-width: 8px;
    }
    .settings {
      width: 25px;
    }
  }
</style>
