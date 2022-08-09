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
<!-- 
  notes
  pwa?
  form input binding ?
  api
  https://cn.vuejs.org/api/composition-api-setup.html

  Vue Router?
  Axios in Vue3 ?
  https://cn.vuejs.org/guide/essentials/application.html#mounting-the-app

  pwa?

  axios
  https://www.youtube.com/watch?v=yNrqlxn0nc0
  https://developer.school/how-to-use-vue-js-json-server-and-axios

  api diff
  https://www.sitepoint.com/vue-composition-api-reusable-components/#:~:text=The%20Composition%20API%20is%20a,and%20shared%20between%20different%20projects.
  in vue


  hko
  https://www.hko.gov.hk/tc/weatherAPI/doc/files/HKO_Open_Data_API_Documentation_tc.pdf
  mtr
  https://opendata.mtr.com.hk/doc/Next_Train_DataDictionary_v1.2.pdf
 -->
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
