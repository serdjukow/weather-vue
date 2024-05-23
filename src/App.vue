<script>
import axios from "axios"

export default {
  data() {
    return {
      city: "",
      error: "",
      info: null,
      apiKey: "fb7e9625cb6c8a4f5a7a4aa5fd58f198",
    }
  },
  computed: {
    cityName() {
      return `"${this.city}"`
    },
    showTemp() {
      return this.info.main.temp
    },
    showFeelsLike() {
      return this.info.main.feels_like
    },
    showMinTemp() {
      return this.info.main.temp_min
    },
    showMaxTemp() {
      return this.info.main.temp_max
    },
    showIcon() {
      return `http://openweathermap.org/img/wn/${this.info.weather[0].icon}.png`
    },
    showDescription() {
      return this.info.weather[0].description
    },
    showTitle() {
      return this.info.weather[0].name
    },
  },
  methods: {
    getWeathers() {
      if (this.city.trim().length < 2) {
        this.error = "Please add city"
        return false
      }
      this.error = ""

      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${this.apiKey}`
        )
        .then((response) => (this.info = response.data))
    },
  },
}
</script>

<template>
  <div class="container">
    <main class="page">
      <div class="app">
        <header class="app__header">
          <h1>Weather</h1>
          <p>Get weather in {{ city == "" ? "your city" : cityName }}</p>
        </header>
        <div class="app__body">
          <input
            type="text"
            v-model="city"
            class="app__input"
            placeholder="add city"
          />
          <button
            v-if="city != ''"
            @click="getWeathers()"
            id="button"
            class="app__btn"
          >
            Go
          </button>
          <button disabled v-else="city != ''" id="button" class="app__btn">
            Add city
          </button>
          <p class="app__error">{{ error }}</p>
          <div v-if="info != null" class="weather-card">
            <div class="weather-card-header">
              <h1>{{ city }}</h1>
              <img :src="`${showIcon}`" alt="" />
            </div>
            <div class="weather-card-current-temp">
              <span>{{ showTemp }}°C</span>
            </div>
            <h2>{{ showDescription }}</h2>
            <p>
              Feels Like: <span>{{ showFeelsLike }}°C</span>
            </p>
            <p>
              Min Temp: <span>{{ showMinTemp }}°C</span>
            </p>
            <p>
              Max Temp: <span>{{ showMaxTemp }}°C</span>
            </p>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<style scoped>
.weather-card {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 20px;
  text-align: center;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.15);
  min-width: 200px;
  margin: auto;

}
  .weather-card-header {
    display: flex;
    justify-content
    : center;
  }
.weather-card h1 {
  font-size: 20px;
  margin: 10px 0;
  text-transform: capitalize;
}
.weather-card h2 {
  font-size: 16px;
  margin: 10px 0;
  text-transform: capitalize;
}
.weather-card-current-temp {
  font-size: 22px;
  color: tomato;
  font-weight: bold;
}
.weather-card p {
  margin: 10px 0;
  font-size: 16px;
}
.weather-card p span {
  
  color: tomato;
}
.weather-card img {
  height: 50px;
  width: 50px;
}
</style>
