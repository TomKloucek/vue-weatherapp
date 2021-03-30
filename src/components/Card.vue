<template>
  <div class='card'>
      <h2>{{ Math.round(data.temp.day)+'°' }}</h2>
      <img :src="require(`../assets/img/${image}`)"/>
      <h5>{{ new Date(data.dt * 1000).toLocaleString("default", { weekday: "long" }) }}</h5>
  </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['data'],
    computed: {
        image() {
            const pocasi = this.data.weather[0].description;
            switch (pocasi) {
                case 'overcast clouds':
                    return 'overcast-broken.svg';
                case 'broken clouds':
                    return 'overcast-broken.svg';
                case 'scattered clouds':
                    return 'overcast-broken.svg';
                case 'light snow': 
                    return 'snow.svg'
                case 'rain and snow':
                    return 'snow.svg'
                case 'moderate rain':
                    return 'rain.svg'
                case 'light rain':
                    return 'lightrain.svg'
                case 'clear sky':
                    return 'clear.svg'
                case 'few clouds':
                    return 'fewclouds.svg'
                default:
                    return 'sunset.svg'
            }     
        }
    }
}
</script>

<style scoped>
.card {
    height: 130px;
    background-color: #333538;
    width: 10%;
    border-top: 5px solid #FFBE00;
    border-radius: 5px;
    transition: all .1s ease-in-out;
}

img {
    width:70px;
    height:70px;
}

.card:hover {
  transform: scale(1.2);
}
</style>