<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from './components/HelloWorld.vue'
import { ref } from 'vue'
import axios from 'axios'
const weatherAPIData = ref()
const mtrAPIData = ref()
const name = ref("")
const age = ref("")
const selected = ref("")

const HKOPath = 'https://data.weather.gov.hk/weatherAPI/opendata/weather.php'
const MTRPath = 'https://rt.data.gov.hk/v1/transport/mtr/getSchedule.php'
const GetHKO = () => {
  axios.get(HKOPath, {
    params: {
      dataType: "flw",
      lang: "tc",
    }
  })
    .then(function (response) {
      console.log("response", response);
      console.log("response.data", response.data);
      weatherAPIData.value = response.data
    })
    .catch(function (error) {
      console.log("axios error", error);
    });
}
const GetMTR = () => {
  axios.get(MTRPath, {
    params: {
      line: "EAL",
      sta: "SHT",
      lang: "TC",
    }
  })
    .then(function (response) {
      console.log("response", response);
      console.log("response.data", response.data);
      mtrAPIData.value = response.data
    })
    .catch(function (error) {
      console.log("axios error", error);
    });
}

GetHKO()
GetMTR()

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
  <h1>get data from API</h1>
   <div>
    <button @click="GetHKO">GetHKO</button>
  </div>
  <table v-if="weatherAPIData">
    <tr>
      <th colSpan = "2">{{ weatherAPIData.forecastPeriod }}</th>
    </tr>
    <tr>
      <td>updateTime</td>
      <td>{{ weatherAPIData.updateTime }}</td>
    </tr>
    <tr>
      <td>forecastDesc</td>{{ weatherAPIData.forecastDesc }}<td></td>
    </tr>
    <tr>
      <td>outlook</td>
      <td>{{ weatherAPIData.outlook }}</td>
    </tr>
  </table>

<br>

   <div>
    <button @click="GetMTR">GetMTR</button>
  </div>
  <table v-if="mtrAPIData">
    <tr>
      <td>message</td>
      <td style="font-weight: bold; color: greenyellow;">{{ mtrAPIData.message.toUpperCase() }}</td>
    </tr>
    <tr>
      <td>最後更新日期</td>
      <td>{{ mtrAPIData.curr_time }}</td>

    </tr>
    <tr>
      <td>status</td>
      <td v-if="mtrAPIData.status" style="font-weight: bold; color: greenyellow;">Normal</td>
      <td v-else style="font-weight: bold; color: red;">Error</td>
    </tr>
    <tr>
      <td>isdelay</td>
      <td v-if="mtrAPIData.isdelay == 'N'" style="font-weight: bold; color: greenyellow;">No delay</td>
      <td v-else style="font-weight: bold; color: red;">Delay</td>
    </tr>
    <tr>
      <td colspan="2">{{ JSON.stringify(mtrAPIData.data) }}</td>
    </tr>
  </table>
<br>

<form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Name</label>
      <input type="text" v-model="name" name="name" placeholder="Enter Your Name" />
    </div>
    <div class="form-control">
      <label>Age</label>
      <input
        type="text"
        v-model="age"
        name="age"
        placeholder="Enter Your Age"
      />
      <select v-model="selected">
        <option disabled value="">Please select one</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
      </select>
    </div>
    <input type="submit" value="Save Information" class="btn btn-block" />
  </form>
  <div>
    {{name}}
    {{age}}
    {{selected}}
  </div>
</template>

<style scoped>
table{
  border: 1px yellow solid;
}
td:first-child{
  width: 25%;
}
</style>
