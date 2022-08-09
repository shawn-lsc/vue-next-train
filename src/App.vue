<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from './components/HelloWorld.vue'
import {ref} from 'vue'
import axios from 'axios'
const weatherAPIData= ref()

const HKOPath = 'https://data.weather.gov.hk/weatherAPI/opendata/weather.php'
axios.get(HKOPath, {
  params: {
    dataType: "flw",
    lang: "tc"
  }
})
.then(function (response) {
  console.log("response",response);
  console.log("response.data",response.data);
  weatherAPIData.value = response.data
})
.catch(function (error) {
  console.log("axios error",error);
});
</script>

<template>
  <!-- <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" /> -->
  <h1>API</h1>
  <table v-if="weatherAPIData">
    <tr>
      <td>updateTime</td>
      <td >{{weatherAPIData.updateTime}}</td>
    </tr>
  </table>


</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
