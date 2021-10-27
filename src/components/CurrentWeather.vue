<template>
  <div class="container">
    <div class="currentWeather" v-if="cityWeather">
      <div class="search-wrapper">
        <input v-model.lazy="searchBar" v-on:keyup.enter="searchCity()" class="search-input" placeholder="Enter City Name">
        <button class="search-button" v-on:click="searchCity()">
          <i class="fa fa-search-location"></i>
        </button>
      </div>
      <div class="current-location-warpper">
        <div class="weather-icon-container">
          <div v-if="clearSky.includes(this.cityWeather['temp_icon'])">
            <div class="hot">
              <span class="sun"></span>
              <span class="sunx"></span>
            </div>
          </div>

          <div v-if="cloudy.includes(this.cityWeather['temp_icon'])">
            <div class="cloudy">
              <span class="cloud"></span>
              <span class="cloudx"></span>
            </div>
          </div>

          <div v-if="snow.includes(this.cityWeather['temp_icon'])">
            <div class="stormy">
              <ul>
              <li></li>
              <li></li>
              <li></li>
              <li></li>
              <li></li>
              <li></li>
              <li></li>
              <li></li>
              </ul>
              <span class="snowe"></span>
              <span class="snowex"></span>
              <span class="stick"></span>
              <span class="stick2"></span>
            </div>
          </div>
          
          <div v-if="rain.includes(this.cityWeather['temp_icon'])">
            <div class="breezy">
              <ul>

              <li></li>
              <li></li>
              <li></li>
              <li></li>
              <li></li>	
              </ul>
              <span class="cloudr"></span>
            </div>
          </div>

          <div v-if="night.includes(this.cityWeather['temp_icon'])">
            <div class="night">
            <span class="moon"></span>
            <span class="spot1"></span>
            <span class="spot2"></span>
            <ul>
              <li></li>
              <li></li>
              <li></li>
              <li></li>
              <li></li>	
              </ul>

            </div>
          </div>
        </div>
      </div>
      <div class="location-warpper">
        <h1 class="city-name">{{ this.cityWeather['city_name'] }}<span>, {{ this.cityWeather['timezone'] }}</span></h1>
        <p class="current-timestamp">As on {{ this.cityWeather['current_date'] }} &nbsp;<span v-on:click="getCity()"><i class="fa fa-redo"></i></span></p>
      </div>
      <div class="temp-wrapper">
        <h1 class="temp">{{ this.cityWeather['current_temp'] }}°</h1>
        <p class="temp-desc">{{ this.cityWeather['desc'] }}</p>
        <p class="feels"> {{ this.cityWeather['city_name'] }} Feels like : {{ this.cityWeather['temp_f'] }}°</p>
      </div>
      <div class="additional-info-wrapper">
        <p class="sunriseTime"><i class="wi wi-sunrise"></i><span>{{ this.cityWeather['sunrise'] }}</span></p>
        <p class="sunsetTime"><i class="wi wi-sunset"></i><span>{{ this.cityWeather['sunset'] }}</span></p>
        <p class="celsius"><i class="wi wi-thermometer"></i><span>{{ this.cityWeather['temp_c'] }}</span><i class="wi wi-celsius"></i></p>
        <p class="fahrenheit"><i class="wi wi-thermometer"></i><span>{{ this.cityWeather['temp_f'] }}</span><i class="wi wi-fahrenheit"></i></p>
      </div>
    </div>
    <div class="currentStats"  v-if="cityWeather">
      <div class="stats-container">
        <p class="title">Today's Highlight</p>
        <div class="stats-wrapper">
          <table>
            <tbody>
              <tr>
                <td><i class="wi wi-thermometer"></i></td>
                <td id='metric'>High</td>
                <td id='value'>{{ this.cityWeather['temp_max'] }}°</td>
                <td><i class="wi wi-thermometer"></i></td>
                <td id='metric'>Low</td>
                <td id='value'>{{ this.cityWeather['temp_min'] }}°</td>
              </tr>
              <tr>
                <td><i class="wi wi-humidity"></i></td>
                <td id='metric'>Humidity</td>
                <td id='value'>{{ this.cityWeather['humidity'] }} %</td>
                <td><i class="wi wi-dust"></i></td>
                <td id='metric'>Visibility</td>
                <td id='value'>{{ this.cityWeather['visibility']/1000 }} km</td>
              </tr>
              <tr>
                <td><i class="wi wi-horizon-alt"></i></td>
                <td id='metric'>UV Index</td>
                <td id='value'>{{ this.cityWeather['uvi'] }}</td>
                <td><i class="wi wi-strong-wind"></i></td>
                <td id='metric'>Wind Speed</td>
                <td id='value'>{{ this.cityWeather['wind_speed'] }} km/h</td>
              </tr>
              <tr>
                <td><i class="wi wi-barometer"></i></td>
                <td id='metric'>Pressure</td>
                <td id='value'>{{ this.cityWeather['pressure'] }}</td>
                <td><i class="wi wi-raindrops"></i></td>
                <td id='metric'>Dew Point</td>
                <td id='value'>{{ this.cityWeather['dew_point'] }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <div class="allWeather"  v-if="cityWeather">
      <div class="tab-container">
        <button id="hourly" @click="displayHourly()">Hourly</button>
        <span>|</span>
        <button id="daily" @click="displayDaily()">Daily</button>
      </div>
      <div class="hourly-container" v-bind:style="{ display: this.tab1Display }">
        <ul class="list">
          <li class="list-item active">
              <div class="icon"><img id="wicon" :src="this.cityWeather['hourly_icon_0']" alt="Weather icon"></div>
              <div class="metric">{{ this.cityWeather['hourly_time_0'] }}</div>
              <div class="temp-new">{{ this.cityWeather['hourly_temp_0'] }}°</div>
          </li>
          <li class="list-item">
              <div class="icon"><img id="wicon" :src="this.cityWeather['hourly_icon_1']" alt="Weather icon"></div>
              <div class="metric">{{ this.cityWeather['hourly_time_1'] }}</div>
              <div class="temp-new">{{ this.cityWeather['hourly_temp_1'] }}°</div>
          </li>
          <li class="list-item">
              <div class="icon"><img id="wicon" :src="this.cityWeather['hourly_icon_2']" alt="Weather icon"></div>
              <div class="metric">{{ this.cityWeather['hourly_time_2'] }}</div>
              <div class="temp-new">{{ this.cityWeather['hourly_temp_2'] }}°</div>
          </li>
          <li class="list-item">
              <div class="icon"><img id="wicon" :src="this.cityWeather['hourly_icon_3']" alt="Weather icon"></div>
              <div class="metric">{{ this.cityWeather['hourly_time_3'] }}</div>
              <div class="temp-new">{{ this.cityWeather['hourly_temp_3'] }}°</div>
          </li>
        </ul>
      </div>
      <div class="daily-container" v-bind:style="{ display: this.tab2Display }">
        <ul class="list">
          <li class="list-item active">
              <div class="icon"><img id="wicon" :src="this.cityWeather['daily_icon_0']" alt="Weather icon"></div>
              <div class="metric">{{ this.cityWeather['daily_day_0'] }}</div>
              <div class="temp-new">{{ this.cityWeather['daily_temp_0'] }}°</div>
          </li>
          <li class="list-item">
              <div class="icon"><img id="wicon" :src="this.cityWeather['daily_icon_1']" alt="Weather icon"></div>
              <div class="metric">{{ this.cityWeather['daily_day_1'] }}</div>
              <div class="temp-new">{{ this.cityWeather['daily_temp_1'] }}°</div>
          </li>
          <li class="list-item">
              <div class="icon"><img id="wicon" :src="this.cityWeather['daily_icon_2']" alt="Weather icon"></div>
              <div class="metric">{{ this.cityWeather['daily_day_2'] }}</div>
              <div class="temp-new">{{ this.cityWeather['daily_temp_2'] }}°</div>
          </li>
          <li class="list-item">
              <div class="icon"><img id="wicon" :src="this.cityWeather['daily_icon_3']" alt="Weather icon"></div>
              <div class="metric">{{ this.cityWeather['daily_day_3'] }}</div>
              <div class="temp-new">{{ this.cityWeather['daily_temp_3'] }}°</div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'CurrentWeather',
  data() {
    return {
      // Search Bar
      searchBar: null,
      city: null,
      // Location Geotaging
      location: null,
      errorStr: null,
      latitude: 0,
      longitude: 0,
      // Open Weather
      apiKey: 'open-weather-map-api',
      weather: {},
      allWeather: {},
      cityWeather: null,
      timestamp: null,
      temperature: null,
      tab1Display:'block',
      tab2Display:'none',
      clearSky: ['01d', '01n', '50d', '50n'],
      cloudy: ['02d', '02n', '03d', '03n', '04d', '04n'],
      snow: ['13d', '13n'],
      rain: ['10d', '10n', '09d', '09n', '11d', '11n'],
      night: [],
    }
  },
  created() {
    this.latitude = this.$cookies.get('latitude');
    this.longitude = this.$cookies.get('longitude');
    console.log(this.longitude)
    if (this.longitude == 0 || this.longitude == null) {
      // Location Geotaging & Cookies
      navigator.geolocation.getCurrentPosition(pos => {
        this.location = pos;
        this.latitude = this.location.coords.latitude;
        this.longitude = this.location.coords.longitude;
        this.getCity()
      }, err => {
        this.errorStr = err.message;
      })
      return this.location
    } else {
      this.getCity()
      return this.latitude
    }
  },
  methods: {
    async searchCity() {
      this.city = this.searchBar;
      // Get City Coordinates
      await axios.get('https://api.openweathermap.org/data/2.5/weather?q='+ this.city +'&appid=' + this.apiKey)
      .then(response => (
        this.weather = response.data,
        this.latitude = this.weather['coord']['lat'],
        this.longitude = this.weather['coord']['lon'],
        this.getWeather(),
        // Cookies
        this.$cookies.set('latitude',this.latitude),
        this.$cookies.set('longitude',this.longitude)
        ))
      .catch(error => (
        alert('City Not Found'), 
        console.log(error),
        this.$cookies.set('latitude',0),
        this.$cookies.set('longitude',0)
        ))
      return this.weather
    },
    async getCity() {
      // Get City Name
      await axios.get('https://api.openweathermap.org/data/2.5/weather?lon=' + this.longitude + '&lat=' + this.latitude +'&appid=' + this.apiKey)
      .then(response => (
        this.weather = response.data,
        this.latitude = this.weather['coord']['lat'],
        this.longitude = this.weather['coord']['lon'],
        this.getWeather()
        ))
      .catch(error => (alert('City Not Found'), console.log(error)))
      return this.weather
    },
    async getWeather() {
      // Get City Weather
      await axios.get('https://api.openweathermap.org/data/2.5/onecall?lon=' + this.longitude + '&lat=' + this.latitude + '&exclude=minutely,alert&appid=' + this.apiKey)
      .then(response => (
        this.allWeather = response.data,
        this.compileWeather(this.weather, this.allWeather),
        this.compileDetailedWeather(this.allWeather)
        ))
      .catch(error => (alert('Something went wrong with the API'), console.log(error)))
      return this.allWeather
    },
    compileWeather(weather, allWeather) {
      this.cityWeather = {}
      this.cityWeather.city_name = weather['name'];
      this.cityWeather.timezone = allWeather['timezone'];
      this.cityWeather.current_date = this.localTime(weather['dt']);
      this.cityWeather.current_temp = this.tempToFahr(allWeather['current']['temp']);
      this.cityWeather.desc = allWeather['current']['weather'][0]['main'];
      this.cityWeather.temp_icon = weather['weather'][0]['icon'];
      this.cityWeather.temp_f = this.tempToFahr(allWeather['current']['temp']);
      this.cityWeather.temp_c = this.tempToCel(allWeather['current']['temp']);
      this.cityWeather.sunrise = this.localTimeHour(allWeather['current']['sunrise']);
      this.cityWeather.sunset = this.localTimeHour(allWeather['current']['sunrise']);
      this.cityWeather.temp_max = this.tempToFahr(weather['main']['temp_max']);
      this.cityWeather.temp_min = this.tempToFahr(weather['main']['temp_min']);
      this.cityWeather.humidity = weather['main']['humidity'];
      this.cityWeather.visibility = weather['visibility'];
      this.cityWeather.uvi = allWeather['current']['uvi'];
      this.cityWeather.wind_speed = allWeather['current']['wind_speed'];
      this.cityWeather.pressure = allWeather['current']['pressure'];
      this.cityWeather.dew_point = allWeather['current']['dew_point'];
    },
    compileDetailedWeather(allWeather) {
      for (let i = 0 ; i <= 3; i++) {
        this.cityWeather["hourly_icon_" + i] = this.getIconUrl(allWeather['hourly'][i]['weather'][0]['icon']);
        this.cityWeather["hourly_time_" + i] = this.localTimeHour(allWeather['hourly'][i]['dt']);
        this.cityWeather["hourly_temp_" + i] = this.tempToFahr(allWeather['hourly'][i]['temp']);
        this.cityWeather["daily_icon_" + i] = this.getIconUrl(allWeather['daily'][i]['weather'][0]['icon']);
        this.cityWeather["daily_day_" + i] = this.localTimeWeek(allWeather['daily'][i]['dt']);
        this.cityWeather["daily_temp_" + i] = this.tempToFahr(allWeather['daily'][i]['temp']['day']);
      }
    },
    localTime(timestamp) {
      this.timestamp = Date(timestamp)
      return this.timestamp
    },
    localTimeHour(timestamp) {
      this.timestamp = new Date(timestamp * 1000)
      return this.timestamp.toLocaleString('en-US', { hour: 'numeric', hour12: true, minute: '2-digit'})
    },
    localTimeWeek(timestamp) {
      this.timestamp = new Date(timestamp * 1000)
      return this.timestamp.toLocaleString('en-US', { weekday: 'short' })
    },
    tempToFahr(temp) {
      this.temperature = temp * 9/5 - 459.67
      return Math.round(this.temperature)
    },
    tempToCel(temp) {
      this.temperature = temp - 273.15
      return Math.round(this.temperature)
    },
    displayHourly() {
      this.tab1Display = 'block'
      this.tab2Display = 'none'
    },
    displayDaily() {
      this.tab1Display = 'none'
      this.tab2Display = 'block'
    },
    getIconUrl(iconCode) {
      this.iconUrl = "https://openweathermap.org/img/w/" + iconCode + ".png";
      return this.iconUrl
    }
  }
}
</script>

<style scoped>
.current-weather-container {
  width: 100%;
}

.search-wrapper {
  border-radius: 30px;
  background-color: #fff;
  padding-right: 12px;
  height: 60px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  color: #1f2937;
  box-shadow: 0 2px 6px 0 rgba(136,148,171,.2),0 24px 20px -24px rgba(71,82,107,.1);
  overflow: hidden;
  box-shadow: #4A4A4A;
  border: 0.1px solid #D6D6D6;
}

.search-input {
  border: none;
  flex: 1;
  outline: none;
  height: 100%;
  padding: 0 20px;
  font-size: 16px;
  background-color: #fff;
  color: #1f1c2e;
  opacity: 0.6;
}

.search-button {
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.search-button i {
  font-size: 30px;
  color: #909090;
}

.location-warpper {
  margin-top: 200px;
}

.city-name > span {
  font-size: 70%;
  font-family: 'Poppins', sans-serif;
  font-weight: 500;
  color: #878686;
}

.current-timestamp {
  margin-top: -15px;
  font-family: 'Poppins', sans-serif;
  font-weight: 500;
  color: #878686;
}

.current-timestamp > span {
  cursor: pointer;
}

.temp {
  margin-top: -15px;
  font-size: 100px;
  color: orange;
}

.temp-desc {
  margin-top: -80px;
  margin-left: 10px;
  font-family: 'Poppins', sans-serif;
  font-weight: 500;
  color: #878686;
  font-size: 20px;
}

.feels {
  margin-top: -10px;
  margin-left: 10px;
  font-family: 'Poppins', sans-serif;
  font-weight: 500;
  color: #878686;
}


.additional-info-wrapper {
  display: flex;
  flex-wrap: wrap;
  margin-left: 10px;
}

.sunriseTime, .sunsetTime, .fahrenheit, .celsius {
  margin-right: 30px;
  font-size: 20px;
  color: #878686;
}

.sunriseTime > i, .sunsetTime > i {
  margin-right: 20px;
}

.fahrenheit > i, .celsius > i {
  margin-right: 20px;
}

.stats-container {
  width: 100%;
}

.stats-container > .title{
  font-family: 'Poppins', sans-serif;
  font-weight: 600;
  color: #878686;
  font-size: 20px;
  margin-bottom: -20px;
}

table { 
  width: 100%; 
  border-collapse: collapse; 
  margin:50px auto;
  }

td { 
  padding: 10px; 
  border-bottom: 1px solid #ccc; 
  text-align: left; 
  font-size: 18px;
  }

td > i {
  color: #878686;
  font-size: 25px;
}

#metric {
  font-family: 'Poppins', sans-serif; 
  font-weight: 600;
  font-size: 15px;
}

#value {
  font-family: 'DM Sans', sans-serif;  
  font-size: 17px;
}

.detailed-weather-container {
  width: 100%;
}

#hourly, #daily {
  background-color: white;
  border: none;
  cursor: pointer;
  font-family: 'Poppins', sans-serif;
  font-size: 15px;
  color: #878686;
  font-weight: 500;
}

#hourly {
  color: #333;
}

.tab-container > span {
  color: #878686;
}

.list {
  display: grid;
  grid-template-columns: repeat(4, auto);
  column-gap: 21px;
  margin-left: -40px;
}

.list-item {
  display: grid;
  justify-items: center;
  padding: 16px 12px;
  border-radius: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
  color: #878686;
}

.list-item.active {
  background-color: blue;
  color: white;
}

#wicon {
  width: 70px;
  height: 70px;
  margin-bottom: -10px;
}

.metric {
  font-size: 20px;
  font-weight: bold;
}

.temp-new {
  margin-top: 5px;
  font-size: 20px;
}

.weather-icon-container > div > div {
  width:130px;
  height:130px;
  border-radius: 40%;
  /* z-index:120; */
}

.hot { 
  display: flex;
  top: 27%;
  position: absolute;
  background:linear-gradient( to top right, rgba(255,87,34,1) 0%,
  rgba(251,140,0 ,1) 100%);
  box-shadow: 1px 1px 30px rgba(255,111,0 ,1);
}

.sun
{
  position: absolute;
  top:-10%;
  left:65%;
  width:50px;
  height: 50px;
  border-radius: 100%;
  background:linear-gradient( to bottom left, rgba(255,235,59,1) 0%,
  rgba(249,168,37 ,1) 90%);
  box-shadow: 1px 1px 30px rgba(255,160,0 ,1);
  animation: inex 3s infinite linear ;
}

.sunx
{
  position: absolute;
  width:10px;
  height: 10px;
  border-radius: 100%;
  background-color: #fff;
  opacity:0.2;
}

.cloudy
{ 
  position: absolute;
  top:27%;
  background:linear-gradient( to top right, rgba(63,81,181,1) 0%,
  rgba(3,155,229 ,1) 40%);
  box-shadow: 1px 1px 30px rgba(2,119,189 ,1);

}
.cloud
{
position: absolute;
  top:5%;
  left:70%;
  width:60px;
  height: 20px;
  border-radius:10px;
  background-color: rgba(129,212,250 ,1);
  box-shadow: 1px 1px 30px rgba(0,151,167 ,1);
animation: move 3s infinite linear ;

}
.cloudx
{
  position: absolute;
  top:23%;
  left:55%;
  width:60px;
  height: 20px;
  border-radius:10px;
  background-color: rgba(129,212,250 ,1);
  animation: move 3s infinite linear ;

}

.stormy
{
  position: absolute;
  top:27%;
  background:linear-gradient( to top right,rgba(117,117,117 ,1) 0%,
  rgba(33,33,33 ,1) 90%);
  box-shadow: 1px 1px 30px rgba(33,33,33 ,1);
}
.stormy li
{
  position: absolute;
  list-style: none;
  width: 5px;
  height: 5px;
  border-radius: 100%;
  background-color:#777;
  box-shadow: 1px 1px 30px #555;
  animation: fall 3s infinite linear ;
opacity:0;
}
.stormy li:nth-child(1)
{
top:0%;
left:100%;
}

.stormy li:nth-child(2)
{
top:5%;
left:90%;
}

.stormy li:nth-child(3)
{
top:-10%;
left:80%;
animation-delay: 2s;
}

.stormy li:nth-child(4)
{
top:10%;
left:100%;
animation-delay: 2s;
}

.stormy li:nth-child(5)
{
top:20%;
left:80%;
animation-delay: 0.5s;
}

.stormy li:nth-child(6)
{
top:35%;
left:70%;
background-color: #bbb;
animation-delay: 0.5s;
}


.stormy li:nth-child(7)
{
top:23%;
left:60%;
background-color: #bbb;
animation-delay: 0.8s;
}

.stormy li:nth-child(8)
{
top:5%;
left:70%;
background-color: #bbb;
animation-delay: 0.8s;
}

.snowe
{
position: absolute;
  top:60%;
  left:40%;
  width:40px;
  height: 40px;
  border-radius:60px;
  background-color: #ddd;
  

}
.snowex
{
  position: absolute;
  top:50%;
  left:50%;
  width:15px;
  height: 15px;	
  border-radius:15px;
  background-color: #bbb;

}
.stick
{
  position: absolute;
  top:60%;
  left:40%;
  width:3px;
  height: 15px;	
  transform: rotate(-45deg);
  background-color: #333;
z-index: -10;
}
.stick2
{
  position: absolute;
  top:60%;
  left:70%;
  width:3px;
  height: 15px;	
  transform: rotate(45deg);
  background-color: #333;
z-index: -10;
}

.breezy
{
  position: absolute;
  top:27%;
  background:linear-gradient( to top right,rgba(156,204,101 ,1) 0%,
  rgba(38,198,218 ,1) 50%);
  box-shadow: 1px 1px 30px rgba(38,198,218 ,1);

}
.cloudr
{
position: absolute;
  top:5%;
  left:60%;
  width:60px;
  height: 20px;
  border-radius:10px;
  background-color: rgba(96,125,139 ,1);
  box-shadow: 1px 1px 30px rgba(84,110,122 ,1);
animation: flash 1.5s infinite linear;

}

.breezy li
{
  position: absolute;
  list-style: none;
  width: 2px;
  height: 7px;
  border-radius: 10%;
  background-color:#eee;
  opacity:0;
  animation: fall 3s infinite linear ;
  transform: rotate(25deg);
}
.breezy li:nth-child(1) {	
  top:10%;
  left:95%;
}

.breezy li:nth-child(2) {
  top:5%;
  left:83%;
  animation-delay:0.3s;
}

.breezy li:nth-child(3) {
  top:4%;
  left:87%;
  animation-delay:0.6s;
}

.breezy li:nth-child(4) {
  top:15%;
  left:70%;
  animation-delay:1s;
}

.breezy li:nth-child(5) {
 top:10%;
  left:75%;
}

.night {
  position: absolute;
  top:27%;
  background:linear-gradient( to bottom right,rgba(63,81,181,1) 0%,
  rgba(171,71,188 ,1) 70%);
  box-shadow: 1px 1px 30px rgba(81,45,168 ,1);

}

.moon {
  position: absolute;
  top:-10%;
  left:65%;
  width:70px;
  height: 70px;
  border-radius: 100%;
  background:rgba(255,241,118 ,1);
  box-shadow: 1px 1px 30px rgba(224,224,224 ,1);
}

.spot1 {
  position: absolute;
  top:0%;
  left:85%;
  width:10px;
  height: 10px;
  border-radius: 100%;
  background-color: #777;
}

.spot2 {
  position: absolute;
  top:30%;
  left:75%;
  width:5px;
  height: 5px;
  border-radius: 100%;
  background-color: #777;
}

.night li {
  position: absolute;
  list-style: none;
  width: 3px;
  height: 3px;
  border-radius: 100%;
  background-color:#fff;
  transform: rotate(45deg);
}
.night li:nth-child(1) {
  top:30%;
  left:65%;
}

.night li:nth-child(2) {
  top:35%;
  left:53%;
}

.night li:nth-child(3) {
  opacity: 0;
  top:20%;
  left:75%;
  width:2px;
  height: 2px;
  animation: meteor 1.5s infinite linear;
  animation-delay: 0.6s;
}

.night li:nth-child(4) {
  top:5%;
  left:50%;
}

.night li:nth-child(5) {
  opacity: 0;
  top:20%;
  left:55%;
  width:1px;
  height: 15px;
  animation: meteor 1.5s infinite linear;
}

/* Responsive/Mobile Friendly */
@media(max-width: 480px) {

  .search-wrapper {
    height: 40px;
  }

  .search-input {
    margin-right: -100px;
  }

  .search-button i {
    font-size: 20px;
    color: #909090;
  }

  .weather-icon-container > div > div {
    margin-top: -30px;
    width: 100px;
    height: 100px;
  }
  .city-name {
    margin-top: -30px;
    font-size: 35px;
  }

  .city-name > span {
    font-size: 40%;
  }

  .current-timestamp {
    margin-top: -20px;
    font-size: 11px;
    line-height: 20px;
  }

  .additional-info-wrapper {
    display: grid;
  }

  .additional-info-wrapper > p {
    margin-top: 0px;
    font-size: 15px
  }

  .stats-container > .title{
    font-size: 15px;
    margin-top: 0px;
    margin-bottom: -20px;
  }

  table {
    margin: 40px -15px 30px -15px;
  }

  #value {
    font-size: 12px;
    padding: 0px;
  }

  #metric {
    font-size: 10px;
  }
  
  td > i {
    font-size: 15px;
  }

  #wicon {
    width: 40px;
    height: 40px;
    margin-bottom: -10px;
  }

  .metric {
    font-size: 8px;
    width: 100%;
    margin-left: 10px;
    align-items: center;
  }

  .temp-new {
    font-size: 15px;
  }

  .list-item {
    padding: 5px 5px;
    border-radius: 10px;
  }
}

/* Animation */
@keyframes inex {
  50% {
    opacity: 0.4;
  }
  60%	{
    opacity: 1;
  }
}
@keyframes move {
  50% {
    transform: translateX(-10px);
  }
}
@keyframes fall {
  10%
  {
    opacity:0.8;
  }
  50% {
    opacity:1;
    transform: translate(-10px,30px);
  }
  100% {
    transform: translate(-25px,70px);
  }
}
@keyframes flash
{
  48% {
    background-color: rgba(96,125,139 ,1);
  }
  50% {
    background-color: #fff;
  }
  55% {
    background-color: rgba(96,125,139 ,1);
  }
  57% {
    background-color: #fff;	
  }
}
@keyframes meteor
{
  10% { 
    opacity: 1;
  }
  80%	{
    left:10%;
    top:75%;
    opacity: 0;
  }
}
</style>