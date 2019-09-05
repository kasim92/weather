<template>
  <div class="container mt-3">

    <div class="card shadow-sm p-3 mb-5 bg-white rounded">
      <div class="card-body">
        <div class="input-group ">
          <div class="input-group-prepend">
            <div class="input-group-text border-0 bg-transparent mr-n5"><i class="iconStyle fa fa-search"></i></div>
          </div>
          <input type="text" class="form-control pl-5 bg-transparent rounded-pill"
                 placeholder="Enter The City Name"
                 aria-describedby="inputGroupPrepend"
                 v-model="cityName"
                 @keyup.enter="getCityWeather">
        </div>
      </div>
    </div>

    <div class="weather-card shadow-sm p-3 mb-5 bg-white rounded text-center">

        <div class="row d-flex align-items-center justify-content-center">
          <div class="col-lg-2 rounded details-card-color mb-3">
            <h5><i class="fa fa-map-marker" aria-hidden="true"></i> {{weatherData.name}}-{{weatherData.sys.country}}</h5>
            <p class="temp ">{{Math.floor(weatherData.main.temp)}}°</p>
          </div>
          <div class="col-lg-2 rounded details-card-color mb-3 ">
                        <img class="img" :src="getWeatherStatusIcon(weatherData.weather[0].icon)" width="150" height="150" alt="No Image Found">
                        <h5 class="">{{weatherData.weather[0].description}}</h5>
          </div>
        </div>

        <div class="row text-center justify-content-center">
          <div class="col-lg-2 mr-2 pt-3 rounded details-card-color">
            <img class="svg-color" :src="require('../assets/svgIcons/breeze.svg')" width="60" height="60" alt="No Image Found">
            <div class="info">
              <p class="lead">Wind</p>
              <h4>{{weatherData.wind.speed}}</h4>
            </div>
          </div>
          <div class="col-lg-2 mr-2 pt-3 rounded details-card-color">
            <img class="svg-color" :src="require('../assets/svgIcons/gauge.svg')" width="60" height="60" alt="No Image Found">
            <div class="info">
              <p class="lead">Pressure</p>
              <h4>{{weatherData.main.pressure}}</h4>
            </div>
          </div>
          <div class="col-lg-2 mr-2 pt-3 rounded details-card-color">
            <img class="svg-color" :src="require('../assets/svgIcons/drop.svg')" width="60" height="60" alt="No Image Found">
            <div class="info">
              <p class="lead">Humidity</p>
              <h4>{{weatherData.main.humidity}}</h4>
            </div>
          </div>
        </div>

    </div>

  </div>
</template>

<script>

  import axios from 'axios'

  export default {
    name: 'HelloWorld',
    data(){
      return{
        appID:'d0a0f308d27f1a0494583bd6f9f2cd10',
        weatherData:null,
        iconWeatherStatus:'cloudy.svg',
        cityName:'',
        lat:'',
        lng:''
      }
    },
    mounted() {
      // axios
      //         .get('http://api.openweathermap.org/data/2.5/weather?q=Baghdad&appid=d0a0f308d27f1a0494583bd6f9f2cd10&units=metric')
      //         .then(data=>(this.weatherData = data.data))

      this.$getLocation({})
              .then(coordinates => {
                this.lat = coordinates.lat;
                this.lng = coordinates.lng;
                axios
                        .get('http://api.openweathermap.org/data/2.5/weather?lat='+this.lat+'&lon='+this.lng+'&units=metric&appid='+this.appID)
                        .then(data=>(this.weatherData = data.data))
                        .catch(err=>console.log(err))
              });

      // axios
      //         .get('http://api.openweathermap.org/data/2.5/weather?lat='+this.lat+'&lon='+this.lng+'&units=metric&appid=d0a0f308d27f1a0494583bd6f9f2cd10')
      //         .then(data=>(this.weatherData = data.data))
      //         .catch(err=>console.log(err))
    },
    methods:{


      getCityWeather(){
        axios
                .get('http://api.openweathermap.org/data/2.5/weather?q='+this.cityName+'&appid=d0a0f308d27f1a0494583bd6f9f2cd10&units=metric')
                .then(data=>(this.weatherData = data.data))
      },
      // getCityWeatherByGps(){
      //   axios
      //           .get('http://api.openweathermap.org/data/2.5/weather?lat='+this.lat+'&lon='+this.lon+'&units=metric')
      //           .then(data=>(this.weatherData = data.data))
      // },
      getWeatherStatusIcon(weatherIconCode){

        switch (weatherIconCode) {
          // clear sky
          case "01d":return require('../assets/svgIcons/day.svg');
            break;
          case "01n":return require('../assets/svgIcons/night.svg');
            break;
          // few clouds
          case "02d":return require('../assets/svgIcons/cloudy-day-1.svg');
            break;
          case "02n":return require('../assets/svgIcons/cloudy-night-1.svg');
            break;
          // scattered clouds
          case "03d":return require('../assets/svgIcons/cloudy-day-2.svg');
            break;
          case "03n":return require('../assets/svgIcons/cloudy-night-2.svg');
            break;
          // broken clouds
          case "04d":return require('../assets/svgIcons/cloudy-day-3.svg');
            break;
          case "04n":return require('../assets/svgIcons/cloudy-night-3.svg');
            break;
          // shower rain
          case "09d":return require('../assets/svgIcons/rainy-2.svg');
            break;
          case "09n":return require('../assets/svgIcons/rainy-4.svg');
            break;
          // rain
          case "10d":return require('../assets/svgIcons/rainy-1.svg');
            break;
          case "10n":return require('../assets/svgIcons/rainy-7.svg');
            break;
          // thunderstorm
          case "11d":return require('../assets/svgIcons/thunder.svg');
            break;
          case "11n":return require('../assets/svgIcons/thunder.svg');
            break;
          // snow
          case "13d":return require('../assets/svgIcons/snowy-3.svg');
            break;
          case "13n":return require('../assets/svgIcons/snowy-5.svg');
            break;
           // mist
          case "50d":return require('../assets/svgIcons/foggy.svg');
            break;
          case "50n":return require('../assets/svgIcons/foggy.svg');
            break;

          default:return require('../assets/svgIcons/day.svg');
        }
      }
    }
  }

</script>

<style scoped>

  .img{
  background-size: contain;

}
  .temp{
  font-size: 90px;
}
  .details-card-color{
  background-color: rgba(255, 255, 255, 0.07);
}
  .svg-color{
    filter: invert(360%) sepia(100%) saturate(100%) hue-rotate(100deg) brightness(100%) contrast(100%);
  }
  .form-control:hover {
    box-shadow: 0 2px 5px rgba(0,0,0, 0.15), 0 1px 4px rgba(0,0,0, 0.20);
  }
  .form-control:focus{
    border: none !important;
    box-shadow: 0 2px 5px rgba(0,0,0, 0.15), 0 1px 4px rgba(0,0,0, 0.20) !important;
  }
  .iconStyle{
  background: #00B4DB;  /* fallback for old browsers */
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

  .weather-card {
    color: white;
    background: linear-gradient(173deg, #2AB2FE, #7AA6F4, #458CFE, #19C7FF);
    background-size: 800% 800%;

    -webkit-animation: AnimationName 30s ease infinite;
    -moz-animation: AnimationName 30s ease infinite;
    animation: AnimationName 30s ease infinite;
  }
  @-webkit-keyframes AnimationName {
    0%{background-position:87% 0%}
    50%{background-position:14% 100%}
    100%{background-position:87% 0%}
  }
  @-moz-keyframes AnimationName {
    0%{background-position:87% 0%}
    50%{background-position:14% 100%}
    100%{background-position:87% 0%}
  }
  @keyframes AnimationName {
    0%{background-position:87% 0%}
    50%{background-position:14% 100%}
    100%{background-position:87% 0%}
  }

  /*.weather-card {*/
  /*  color: white;*/
  /*  background: linear-gradient(117deg, #53a5db, #63b0de, #73bae1, #ecdd64);*/
  /*  background-size: 800% 800%;*/
  /*  -webkit-animation: AnimationName 30s ease infinite;*/
  /*  -moz-animation: AnimationName 30s ease infinite;*/
  /*  animation: AnimationName 30s ease infinite;*/
  /*}*/

  /*@-webkit-keyframes AnimationName {*/
  /*  0%{background-position:0% 31%}*/
  /*  50%{background-position:100% 70%}*/
  /*  100%{background-position:0% 31%}*/
  /*}*/
  /*@-moz-keyframes AnimationName {*/
  /*  0%{background-position:0% 31%}*/
  /*  50%{background-position:100% 70%}*/
  /*  100%{background-position:0% 31%}*/
  /*}*/
  /*@keyframes AnimationName {*/
  /*  0%{background-position:0% 31%}*/
  /*  50%{background-position:100% 70%}*/
  /*  100%{background-position:0% 31%}*/
  /*}*/


</style>
