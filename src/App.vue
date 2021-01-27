<template>
  <div id="app">
    <Modal v-if="modal" />
    <h1>pomodoro</h1>
    <div class="navbar">
      <span class="navbar_item" :class="{ navbar_item__selected : pomodoro }" @click="navbarChoice(1)">pomodoro</span>
      <span class="navbar_item" :class="{ navbar_item__selected : shortBreak }" @click="navbarChoice(2)">short break</span>
      <span class="navbar_item" :class="{ navbar_item__selected : longBreak }" @click="navbarChoice(3)">long break</span>
    </div>
    <div class="compteur">
      <vue-ellipse-progress :progress="progress" color="#f86f6b" emptyColor="transparent" :thickness="10" :size="350">
        <div class="compteur_informations">
          <div class="compteur_temps">
            <p>{{ minutes }}:{{ secondes }}</p>
          </div>
          <div class="compteur_etat">
            <p>pause</p>
          </div>
        </div>
      </vue-ellipse-progress>
    </div>
    <img class="settings" src="@/assets/gear.svg" alt="parametres" @click="modal = !modal">
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
      minutes: 17,
      secondes: 59,
      progress: 85,
      modal: false,
      poppins: true,
      oswald: false,
      roboto: false,
      saumon: true,
      bleu: false,
      violet: false
    }
  },
  methods: {
    navbarChoice(item) {
      this.pomodoro = false
      this.shortBreak = false
      this.longBreak = false
      if(item == 1) {
        this.pomodoro = true
      }
      else if(item == 2) {
        this.shortBreak = true
      }
      else if(item == 3) {
        this.longBreak = true
      }
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Londrina+Solid&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@700&family=Poppins:wght@700&display=swap');
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
      background-color: #f86f6b;
      border-radius: 50px;
      transition: ease 0.5s;
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
    position: absolute;
    width: 30px;
    bottom: 50px;
    left: calc(50% - 15px);
    cursor: pointer;
  }
</style>
