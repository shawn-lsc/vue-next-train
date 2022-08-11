<template lang="">
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
      <th colspan="3"><h4>EAL-SHT</h4></th>
    </tr>
    <tr>
      <td>目的地</td>
      <td>月台</td>
      <td>下一班車</td>
    </tr>
    <tr 
      v-for='(UP, index) in mtrAPIData.data["EAL-SHT"].UP' 
      :key='UP.seq' >
    <td>{{ UP.dest }}</td>
    <td>{{ UP.plat }}</td>
    <td>{{ UP.ttnt }}</td>
  </tr>
     <tr>
      <td>目的地</td>
      <td>月台</td>
      <td>下一班車</td>
    </tr>
  <tr 
      v-for='(DOWN, index) in mtrAPIData.data["EAL-SHT"].DOWN' 
      :key='DOWN.seq' >
    <td>{{ DOWN.dest }}</td>
    <td>{{ DOWN.plat }}</td>
    <td>{{ DOWN.ttnt }}</td>
  </tr>
  </table>
  <table v-if="mtrAPIData">
    
  </table>
</template>
<script setup lang="ts">
import { ref, reactive } from 'vue'
import axios from 'axios'
const mtrAPIData = ref()
const upList = ref()

const MTRPath = 'https://rt.data.gov.hk/v1/transport/mtr/getSchedule.php'
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
      mtrAPIData.value = response.data;
    })
    .catch(function (error) {
      console.log("axios error", error);
    });
}
GetMTR()

</script>
<style lang="scss" scoped>
table {
  border: 1px red solid;

  td:first-child {
    width: 25%;
  }
}
</style>