<template>
  <div class="app container mt-4">
    <h1>Convertidor de Temperatura</h1>
    <h2>Alumna: Daniela Franco</h2>
    <a href="https://github.com/danielafranc/daniela-franco-parcial-pnt2">Repositorio en GitHub</a>
    <hr>
    <div>
      <form @submit.prevent class="mb-4">
        <label for="celsius">Ingresar Temperatura</label>
        <input 
          type="number" 
          id="celsius"
          v-model.number="temperaturaCelsius"
          name="celsius"
          class="form-control d-inline-block w-25 ms-2"
          required>
      </form>

      <div class="resultados">
        <table class="table table-bordered">
          <thead class="table-light">
            <tr>
              <th>Escala</th>
              <th>Temperatura</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Fahrenheit</td>
              <td :style="{ color: colorTemperatura }">{{temperaturaFahrenheit}}°F</td>
            </tr>
            <tr>
              <td>Kelvin</td>
              <td :style="{ color: colorTemperatura }">{{temperaturaKelvin}}°K</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <Respuestas />
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import Respuestas from './components/Respuestas.vue';

export default {
  components: {
    Respuestas
  },
  setup() {
    const temperaturaCelsius = ref(0);

    const temperaturaFahrenheit = computed(() => {
      return (temperaturaCelsius.value * 9/5) + 32;
    });

    const temperaturaKelvin = computed(() => {
      return temperaturaCelsius.value + 273.15;
    });

    const colorTemperatura = computed(() => {
      if (temperaturaCelsius.value <= 0) {
        return 'blue';
      } else if (temperaturaCelsius.value > 0 && temperaturaCelsius.value < 15) {
        return 'magenta';
      } else {
        return 'red';
      }
    });

    return {
      temperaturaCelsius,
      temperaturaFahrenheit,
      temperaturaKelvin,
      colorTemperatura
    };
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>