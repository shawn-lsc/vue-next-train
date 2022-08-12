<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HKOInfo from './components/HKOInfo.vue';
import MtrNextTrain from './components/MtrNexttrain.vue';
import CryptoPrice from './components/CryptoPrice.vue';
import TestForm from './components/TestForm.vue';

</script>

<template>
  <TestForm></TestForm>
  <h1>get data from API</h1>
  <CryptoPrice></CryptoPrice>
  <HKOInfo></HKOInfo>
  <br>
  <MtrNextTrain></MtrNextTrain>
  <br>
</template>

<style lang="scss">
table {
  border: 1px yellow solid;

  td:first-child {
    width: 25%;
  }
}
</style>
