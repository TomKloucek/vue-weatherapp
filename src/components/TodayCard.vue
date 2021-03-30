<template>
  <div class='today'>
      <div class='container'>
        <div class='leva'>
          <h3>Today</h3>
          <h3>{{(new Date()).toISOString().slice(0, 10).replace(/-/g, "-").replace("T", " ") }}</h3>
        </div>
        <h4>{{ Math.round(data.temp)+'°C' }}</h4>
      </div>
      <div class='container'>
        <div class='detaily'>
            <p>{{'Feels like: '+Math.round(data.feels_like)+'°C'}}</p>
            <p>{{'Humidity: '+data.humidity}}</p>
            <p>{{'Pressure: '+data.pressure+' hPa'}}</p>
            <p>{{'Wind speed: '+data.wind_speed}}</p>
        </div>
        <img :src="require(`../assets/img/${actual}`)">
      </div>
      <div class='sun-container'>
        <div class='sunrise'>
          <p>{{'Sunrise: '+(new Date(data.sunrise*1000)).toISOString().slice(10, 16).replace(/-/g, "-").replace("T", " ")}}</p>
          <img src='../assets/img/sunrise.svg'/>
        </div>
        <div class='sunset'>
          <p>{{'Sunset: '+(new Date(data.sunset*1000)).toISOString().slice(10, 16).replace(/-/g, "-").replace("T", " ")}}</p>
          <img src='../assets/img/sunset.svg'/>
        </div>
      </div>
  </div>
</template>

<script>
export default {
 name: 'Today',
 props: ['data'],
 computed: {
   actual() {
     const pocasi = this.data.weather[0].description;
            switch (pocasi) {
                case 'overcast clouds':
                    document.body.style.background = "#a7a7c2;";
                    return 'overcast-broken.svg';
                case 'broken clouds':
                    document.body.style.background = "#a7a7c2;";
                    return 'overcast-broken.svg';
                case 'scattered clouds':
                    document.body.style.background = "#a7a7c2;";
                    return 'overcast-broken.svg';
                case 'light snow': 
                    document.body.style.background = "#d7dade";
                    return 'snow.svg'
                case 'rain and snow':
                    document.body.style.background = "#d7dade";
                    return 'snow.svg'
                case 'moderate rain':
                    document.body.style.background = "#606d7d";
                    return 'rain.svg'
                case 'light rain':
                    document.body.style.background = "#606d7d";
                    return 'lightrain.svg'
                case 'clear sky':
                    var hr = (new Date()).getHours();
                    if (hr > 20 || hr < 6){
                      document.body.style.background = "#4b4b61";
                      return 'moonsky.svg'
                    }
                    document.body.style.background = "#8eb1e6";
                    return 'clear.svg'
                case 'few clouds':
                    document.body.style.background = "#b2c3d9";
                    return 'fewclouds.svg'
                default:
                    return 'sunset.svg'
            }
   }
 }
}
</script>

<style scoped>
.today {
  padding-top: 2px;
  width: 30%;
  height: 250px;
  background-color: #333538;
  border-top: 5px solid #FFBE00;
  border-radius: 5px;
}
img {
    height: 80px;
    width: 80px;
}

h4 {
  font-size: 50px;
}

.sun-container {
  margin-top: 5px;
  display: flex;
  align-content: space-between;
}

.sunrise > img {
  height: 60px;
  width: 60px;
}

.sunset > img {
  height: 60px;
  width: 60px;
}
</style>