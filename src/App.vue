<template>
  <div class="main-container">
    <CurrentWeather></CurrentWeather>
    <footer>
      <p>
        Designed & Developed with <i class="fa fa-heart"></i> by <b>Akash Sahu</b>
        | Powered by
        <a target="_blank" href="https://openweathermap.org/">OpenWeatherMap</a>.
      </p>
    </footer>
  </div>
</template>

<script>
// import axios from "axios";
import CurrentWeather from './components/CurrentWeather.vue'

export default {
  name: 'App',
  components: {
    CurrentWeather,
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=DM+Sans:400,500,700,900&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800;900&display=swap');

* {
  box-sizing: border-box;
}

body{
  font-family: 'DM Sans', sans-serif;
  background-color: #f3f6fd;
}

.container {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  height: 700px;
  width: 95%;
  margin: auto;
  padding: 20px;
  margin-top: 60px;
}

.currentStats, .allWeather {
  flex: 1;
  width: 50%;
}

.currentWeather {
  background-color: #fff;
  flex: 0 0 100%;
  width: 50%;
  border-radius: 32px;
  padding: 32px 50px 10px 50px;
  overflow: hidden;
  flex-direction: column;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
}

.currentStats {
  background-color: #fff;
  flex: 20%;
  margin-left: 24px;
  padding: 32px 32px 0px 32px;
  border-radius: 32px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
}

.allWeather {
  background-color: #fff;
  margin-left: 24px;
  margin-top: 24px;
  padding: 32px 32px 0px 32px;
  border-radius: 32px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
}

footer {
  width: 100%;
  text-align: center;
  color: #878686;
}

footer i {
  color: red;
}

footer a {
  color: #878686;
  text-decoration: none;
}

@media(max-width: 480px) {
  .container {
    display: flex;
    flex-direction: row;
  }

  .currentWeather, .currentStats, .allWeather {
    flex: 1;
    width: 100%;
  }
  .currentWeather {
    margin: -50px 0px 0px 0px;
    padding: 30px 30px 10px 30px;
    flex: 2;
  }
  .currentStats {
    flex: 5;
    margin: 20px 0px 0px 0px;
  }
  .allWeather {
    flex: 1;
    margin: 20px 0px 30px 0px;
    padding: 20px 20px 10px 20px;
  }

  footer {
    clear: both;
    position: relative;
    margin-top: 470px;
    font-size: 15px;
    line-height: 2;
  }
}
</style>