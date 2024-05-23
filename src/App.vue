<script>
export default {
  data() {
    return {
      city: "",
      error: "",
    }
  },
  computed: {
    cityName() {
      return `"${this.city}"`
    },
  },
  methods: {
    getWeathers() {
      if (this.city.trim().length < 2) {
        this.error = "Please add city"
        return false
      }
      this.error = ""
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
          <p>Get weather in {{ city == "" ? "youre city" : cityName }}</p>
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
        </div>
      </div>
    </main>
    <footer class="footer">footer</footer>
  </div>
</template>
