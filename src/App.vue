<template>
  <header class="header">
    <div class="container">
      <nav class="navbar">
        <div class="logo__container">
          <a class="header__logo navbar-brand mr-3" href="#">Check the Weather</a>
        </div>

        <form class="d-flex">
          <select
            class="select-language form-select"
            aria-label="Default select example"
            v-model="lang"
          >
            <option value="ru">ru</option>
            <option value="eng">eng</option>
          </select>
          <!-- @input="city = $event.target.value" -->

          <el-input
            @keyup.enter.prevent="getWeatherInfo"
            type="search"
            placeholder="Введите город"
            aria-label="Search"
            v-model="city"
            @input="сheckBtn"
          />
          <button
            @click="getWeatherInfo"
            class="btn btn-outline-success show-btn"
            type="button"
            :disabled="!checkInput"
          >Узнать</button>
          <el-button type="text" disabled>Text Button</el-button>
        </form>
      </nav>
    </div>
  </header>
  <div class="content">
    <weather-display
      v-if="info"
      :temp="result.main.temp"
      :sunrise="sunrise"
      :sunset="sunset"
      :temp-min="tempMin"
      :temp-max="tempMax"
      :wind-speed="result.wind.speed"
      :lang="lang"
    ></weather-display>
    <time-of-day v-if="info" :check-sun="checkSun"></time-of-day>

    <div class>{{ result }}></div>

    <!-- <lottie-animation
    path="./assets/sun.json"
    />-->

    <!-- <lottie-animation
  ref="anim"
  :animationData="require('@/assets/sun.json')"
    />-->

    <!-- <div >{{ result }}</div>
    <div>{{ currentTime }}</div>-->
    <page-not-found v-if="errorComponent"></page-not-found>
    <el-button type="text">Text Button</el-button>
    <div>{{ timeNow }}</div>
  </div>
</template>

<script>
import axios from 'axios'
import WeatherDisplay from './components/WeatherDisplay.vue'
import TimeOfDay from './components/TimeOfDay.vue'
import PageNotFound from './components/PageNotFound.vue'
// import LottieAnimation from "lottie-vuejs/src/LottieAnimation.vue"; 
// import {LottieAnimation} from 'lottie-web-vue'
// 5363dff9978d55b37c53e8a1b5e0ffe9
export default {
  components: {
    //  LottieAnimation,
    WeatherDisplay,
    TimeOfDay,
    PageNotFound
  },
  data: () => {
    return {
      city: '',
      result: {},
      sunrise: '',
      sunset: '',
      // currentTime: parseInt(new Date().getTime() / 1000),
      // currentTime:'',
      // sun: true,
      lang: 'ru',
      // temp: '',
      info: false,
      tempMax: '',
      tempMin: '',
      errorComponent: false,
      checkInput: false,

      // windSpeed: ''

    }
  },
  methods: {
    getWeatherInfo() {
      if (this.city.length > 2) {
        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=1aeb00a26f09e25370d11fe4e01edbc5&units=metric&lang=${this.lang}`).then(val => {
          console.log(val)
          this.result = val.data
          this.sunrise = this.result.sys.sunrise
          this.sunset = this.result.sys.sunset
          // this.temp = this.result.main.temp
          this.tempMax = this.result.main.temp_max
          this.tempMin = this.result.main.temp_min
          // this.windSpeed = this.result.wind.speed

          // this.currentTime = this.currentTime.getTimezoneOffset(this.result.timezone)
          console.log(this.currentTime)
          console.log(this.sunrise)
          console.log(this.sunset)
          this.info = true
          if (this.currentTime > this.sunset) this.sun = false

        })
          .catch(function (error) {
            if (error.response.status == '404') {

              this.errorComponent = true
            }

          })
      }
    },
    buttonClicked() {
      this.$refs.anim.play()

    },
    сheckBtn() {

      if (this.city.length > 2) {

        this.checkInput = true
      }
      else this.checkInput = false
    }
  },
  computed: {
    checkSun() {
      // this.checkInput = true
      if (this.currentTime > this.sunrise || this.currentTime < this.sunset) {
        return true
      }
      else {
        return false
      }
    },
    timeNow() {
      const currentTime = new Date((this.result?.sys?.sunrise) * 1000).toUTCString()
      return currentTime
    }

  },
  updated() {
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
:root {
  --main-color: #a08fd5;
  --text-color: #f5e866;
}
.header {
  position: sticky;
  top: 0;

  background-color: #60b683;
  background-color: var(--main-color);
}
.header__logo.navbar-brand {
  color: var(--text-color) !important;
  font-weight: bold;
  font-family: "BhuTuka Expanded One", cursive;
}
.content {
  /* background: url(./assets/photo-1505322022379-7c3353ee6291.jpg) no-repeat;
  background-size: cover; */
  /* background-color: #5B7A97; */
  height: 100vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.navbar {
  display: flex;
  justify-content: space-between;
}
.show-btn {
  color: black;
  background-color: #fff;
  border: none;
}
.show-btn:active {
  outline: none;
}
.show-btn:hover {
  background-color: var(--text-color);
}
input:active,
input:focus {
  box-shadow: 0 0 0 0.25rem var(--text-color) !important;
  box-shadow: unset;
}
.select-language {
  width: unset;
  margin-right: 10px;
}
.form-select:focus {
  border-color: unset;
  outline: 0;
  box-shadow: unset;
  border: unset;
}
.sun {
  width: 200px;
  height: 200px;
  position: absolute;
  animation-name: sun;
  animation-duration: 6s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
}
@keyframes sun {
  0% {
    transform: translate(0px, 0px);
  }
  25% {
    transform: translate(100px, 100px);
  }
  50% {
    transform: translate(0px, 200px);
  }
  75% {
    transform: translate(-100px, 100px);
  }
  100% {
    transform: translate(0px, 0px);
  }
}

.sun-core {
  width: 60px;
  height: 60px;
  background: radial-gradient(
    circle,
    rgba(255, 255, 238, 1) 0%,
    rgba(255, 252, 0, 1) 100%
  );
  box-shadow: 0px 0px 25px 10px rgba(255, 255, 0, 0.8);
  border-radius: 50%;
  position: absolute;
  inset: 65px 65px;
}
.sun-ray {
  width: 4px;
  height: 40px;
  background-color: yellow;
  border-radius: 5px;
  position: absolute;
}
.sun-ray-1 {
  inset: 20px 93px;
}
.sun-ray-2 {
  inset: 130px 93px;
}
.sun-ray-3 {
  inset: 75px 38px;
  transform: rotate(90deg);
}
.sun-ray-4 {
  inset: 75px 148px;
  transform: rotate(90deg);
}
.sun-ray-5 {
  inset: 35px 55px;
  transform: rotate(135deg);
}
.sun-ray-6 {
  inset: 114px 134px;
  transform: rotate(135deg);
}
.sun-ray-7 {
  inset: 35px 134px;
  transform: rotate(45deg);
}
.sun-ray-8 {
  inset: 114px 55px;
  transform: rotate(45deg);
}
</style>