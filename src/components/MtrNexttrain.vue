<template lang="">
  <n-button @click="GetMTR">GetMTR</n-button>
  <div class="mtr">
    <div class="half">
    <h2>left</h2>
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
        <th colspan="3"><h4>EAL- {{sta}}</h4></th>
      </tr>
      <tr>
        <th colspan="3"><h4>UP</h4></th>
      </tr>
      <tr>
        <td>目的地</td>
        <td>月台</td>
        <td>下一班車</td>
      </tr>
      <!-- <tr v-for='(data,index) in mtrAPIData.data["EAL-SHT"]' ::key="key"></tr> -->
      <tr 
        v-for='(UP, index) in mtrAPIData.data["EAL-" + sta].UP' 
        :key='UP.seq' >
      <td>{{ UP.dest }}</td>
      <td>{{ UP.plat }}</td>
      <td>{{ UP.ttnt }}</td>
    </tr>
      <tr>
        <th colspan="3"><h4>DOWN</h4></th>
      </tr>
      <tr>
        <td>目的地</td>
        <td>月台</td>
        <td>下一班車</td>
      </tr>
    <tr 
        v-for='(DOWN, index) in mtrAPIData.data["EAL-"+ sta].DOWN' 
        :key='DOWN.seq' >
      <td>{{ DOWN.dest }}</td>
      <td>{{ DOWN.plat }}</td>
      <td>{{ DOWN.ttnt }}</td>
    </tr>
  </table>
  <table v-if="mtrAPIData">
    
  </table>
  </div>
    <div class="half">
      <h2>right</h2>

      <n-space>
        <n-switch
        checked-value="TC"
        unchecked-value="EN"
        @update:value="handleUpdateValueLang"
        >
          <template #checked> TC</template>
          <template #unchecked>EN</template>
        </n-switch>
      </n-space>
         <n-select v-model:value="value" :options="staList" @update:value="handleUpdateValueSta"/>
      <pre>{{lang}}</pre>
      <pre>{{sta}}</pre>
    </div>
  </div>
  
</template>

<script setup lang="ts">
import axios from 'axios';
import { ref, reactive } from 'vue';
import { NSwitch, NSelect,NButton,NSpace } from 'naive-ui';

const mtrAPIData = ref()
const lang = ref("EN")
const sta = ref('SHS')
const staList = [
{value:'ADM',label:'Admiralty'},
{value:'EXC',label:'Exhibition Centre'},
{value:'HUH',label:'Hung Hom'},
{value:'MKK',label:'Mong Kok East'},
{value:'KOT',label:'Kowloon Tong'},
{value:'TAW',label:'Tai Wai'},
{value:'SHT',label:'Sha Tin'},
{value:'FOT',label:'Fo Tan'},
{value:'RAC',label:'Racecourse'},
{value:'UNI',label:'University'},
{value:'TAP',label:'Tai Po Market'},
{value:'TWO',label:'Tai Wo'},
{value:'FAN',label:'Fanling'},
{value:'SHS',label:'Sheung Shui'},
{value:'LOW',label:'Lo Wu'},
{value:'LMC',label:'Lok Ma Chau'},
]

function handleUpdateValueLang(value: string) {
  lang.value = value;
  GetMTR()
}
function handleUpdateValueSta(value: string) {
  sta.value = value;
  console.log(value)
  GetMTR()
}

const MTRPath = 'https://rt.data.gov.hk/v1/transport/mtr/getSchedule.php'
const GetMTR = () => {
  axios.get(MTRPath, {
    params: {
      line: "EAL",
      sta: sta.value,
      lang: lang.value,
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
GetMTR();

</script>
<style lang="scss" scoped>
table {
  border: 1px red solid;

  th{
    border-top: 1px solid yellow;
  }
}

.mtr {
  display: flex;
}

.half {
  width: 50%;
}
</style>