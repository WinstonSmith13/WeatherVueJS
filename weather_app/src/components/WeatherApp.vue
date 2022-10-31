<template>
  <main>
    <div class="search-box">
      <input
          type="text"
          class="search-bar"
          name="search"
          id="search"
          placeholder="Choisir un lieu"
          v-model="query"
          @keypress="fetchApiWeather"
      />
    </div>

    <div class="weather-wrap">
      <div class="location-box">
        <div class="location">{{ weather.name }}</div>
      </div>

      <div class="weather-box" v-if="typeof weather.main != 'undefined'">
        <div class="temp"> {{ weather.main.temp }}  </div>


        <div class="weather">{{ weather.weather[0].main }}</div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "WeatherApp",
  data() {
    return {
      api_key: '3612570726d94981b3ebe6af117e0346',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },

  methods: {
    fetchApiWeather(e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults (results){
      this.weather = results;
      console.log(results);
    }
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

main {

  font-family: Roboto, sans-serif;
  background-image: url("/src/assets/weather_images.jpeg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  padding: 25px;
  min-height: 100vh;


}

.search-box {
  width: 100%;
  margin-bottom: 30px;

}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  border-radius: 5px;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
}

.location-box .location {
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 1px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  font-size: 22px;
  font-weight: 300;
  text-align: center;
  text-shadow: 1px 1px rgba(0, 0, 0, 0.25);
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: black;
  font-size: 100px;
  font-weight: 900;
  text-shadow: 1px 1px rgba(0, 0, 0, 0.25);

  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.15);
}

.weather-box .weather {
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 1px rgba(0, 0, 0, 0.25);
}

</style>
