<script setup lang="ts">
    import { ref } from 'vue'
    import axios from 'axios'
    const weatherAPIData = ref()

    const HKOPath = 'https://data.weather.gov.hk/weatherAPI/opendata/weather.php'
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
    GetHKO()

</script>


<template>
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
      <td>tcInfo</td>{{ weatherAPIData.tcInfo }}<td></td>
    </tr>
    <tr>
      <td>outlook</td>
      <td>{{ weatherAPIData.outlook }}</td>
    </tr>
  </table>
</template>


<style lang="scss" scoped>
</style>