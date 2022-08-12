<template lang="">
<div class="crypto">
<div class="half">
    <button @Click="Getcryptocompare">update Crypto</button>
</div>
    <div class="half">
        <p>
            <label v-if="btcData">BTC: (USD){{btcData['USD']}}
            <br>(HKD){{btcData['HKD']}}</label>
        </p>
        <p>
            <label v-if="ethData">ETH: (USD){{ethData['USD']}}
            <br>(HKD){{ethData['HKD']}}</label>
        </p>
    </div>
</div>
</template>
<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios';
const btcData = ref()
const ethData = ref()

const cryptocompare = 'https://min-api.cryptocompare.com/data/price'
const Getcryptocompare = () => {
    axios.get(cryptocompare, {
        params: {
            fsym: "ETH",
            tsyms: "USD,HKD",
        }
    })
        .then(function (response) {
            console.log("response", response);
            console.log("response.data", response.data);
            ethData.value = response.data
        })
        .catch(function (error) {
            console.log("axios error", error);
        });
    axios.get(cryptocompare, {
        params: {
            fsym: "BTC",
            tsyms: "USD,HKD",
        }
    })
        .then(function (response) {
            console.log("response", response);
            console.log("response.data", response.data);
            btcData.value = response.data
        })
        .catch(function (error) {
            console.log("axios error", error);
        });
}

Getcryptocompare()
</script>
<style lang="scss">
.crypto{
    display: flex;
    align-items: center;
}
.half {
  width: 50%;
}
</style>