<template>
<!-- ======================================================================= -->
<!-- INLINE JS CHANGES THE DIV CLASS -->
<!-- ======================================================================= -->
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main === 'Clouds' || 'clouds'/ weather.main === 'Clear' || 'clear'/ weather.main ==='undefined' || 'default'">

<!-- ======================================================================= -->
<!-- WARM/COLD -->
<!-- ======================================================================= -->
<!-- <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : 'cold'"> -->

<!-- ======================================================================= -->
<!-- METHOD -->
<!-- ======================================================================= -->
    <!-- <div id="app" :class="getWeatherClass()"> -->
    <main>
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Buscar..."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>
<p class="pregunta">¿Que clima hace en...?</p>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      api_key:'0dd415345fef70ac8ce78ad88d0089c2',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
}
},
methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults (results) {
      console.log(results)
      this.weather = results;
    },

     getWeatherClass () {

if (this.weather && this.weather.weather[0].main === "Clouds") {
return "clouds"}
if(this.weather && this.weather.weather[0].main === "Clear") {
return "clear" }
return "default"},
  
      // if (typeof this.weather != 'undefined'){
      //   return "default";
      // }
      
      // if (this.weather.main === "Clouds"){
      //   return "clouds"
      //   }
        // if (this.weather.main === "Clear"){
        //   return "clear";
        //   }
          // if (this.weather.weather[0].main === "Atmosphere"){
          // return "mist";
          // }
          // if (this.weather.weather[0].main === "Snow"){
          // return "snow";
          // }
          // if (this.weather.weather[0].main === "Rain"){
          // return "rain";
          // }
          // if (this.weather.weather[0].main === "Drizzle"){
          // return "pocorain";
          // }
          // if (this.weather.weather[0].main === "Thunderstorm"){
          // return "tormenta";
          // }
  //       return "default";
  // },
    dateBuilder () {
      let d = new Date();
      let months = ["Enero", "Febrero", "Marzo", "Abril", "Mayo", "Junio", "Julio", "Augusto", "Septiembre", "Octubre", "Noviembre", "Diciembre"];
      let days = ["Domingo", "Lunes", "Martes", "Miércoles", "Jueves", "Viernes", "Sábado"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  },
  
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  }
  body{
font-family: "montserrat", sans-serif;
    }

    #app.cold {
background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  }

  #app.warm {
  background-image: url('./assets/warm-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.default {
background-image: url('./assets/rain-bg.gif');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  }

  #app.clouds {
  background-image: url('./assets/warm-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.clear {
  background-image: url('./assets/clear-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
main{
  min-height:100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.30), rgba(0,0,0,0.70));
  }
  .search-box{
    width:100%;
    margin-bottom: 5px;
    }
    .search-box .search-bar{
      display: block;
      width: 100%;
      padding: 15px;
      position: relative;
      top: 200px;
      color: #313131;
      font-size: 20px;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      box-shadow: 0px 0px 5px rgba(0,0,0,0.25);
      background-color: rgba(255, 255, 255, 0.5);
      border-radius: 4px;
      transition: 0.4s;
      }
      .search-box .search-bar:focus{
        box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
background-color: rgba(255, 255,255, 0.80);
}
.weather-wrap{
  top: 20vh;
    position: relative;
    }
.pregunta{
  font-size: 30px;
  text-align:center;
  color: #ffff;
  position: relative;
  top: 30px;
}
.location-box .location{
  color: #ffffff;
  font-size: 32px;
  font-weight: 500;
  text-align:center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  }
 .location-box .date{
  color: #ffffff;
  font-size: 20px;
  font-weight: 300;
  font-style:italic;
  text-align:center;
  }
.weather-box{
  text-align: center;
  }
  .weather-box .temp{
display: inline-block;
padding: 10px 25px;
color: #fff;
font-size: 90px;
font-weight:lighter;
text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
/* background-color:rgba(204, 238, 238, 0.253); */
    }
    .weather-box .weather{
      color: #ffffff;
      font-size: 40px;
      font-weight: 100;
      font-style: italic;
      text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
      }
</style>

// {
//   "coord": {
//     "lon": -122.08,
//     "lat": 37.39
//   },
//   "weather": [
//     {
//       "id": 800,
//       "main": "Clear",
//       "description": "clear sky",
//       "icon": "01d"
//     }
//   ],
//   "base": "stations",
//   "main": {
//     "temp": 282.55,
//     "feels_like": 281.86,
//     "temp_min": 280.37,
//     "temp_max": 284.26,
//     "pressure": 1023,
//     "humidity": 100
//   },
//   "visibility": 16093,
//   "wind": {
//     "speed": 1.5,
//     "deg": 350
//   },
//   "clouds": {
//     "all": 1
//   },
//   "dt": 1560350645,
//   "sys": {
//     "type": 1,
//     "id": 5122,
//     "message": 0.0139,
//     "country": "US",
//     "sunrise": 1560343627,
//     "sunset": 1560396563
//   },
//   "timezone": -25200,
//   "id": 420006353,
//   "name": "Mountain View",
//   "cod": 200
//   }