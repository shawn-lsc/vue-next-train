<template>
<h1>submit form json</h1>
  <n-form :model="formValue" size="small" :inline="false" :label-width="80" label-align="left" label-placement="left"
    :show-feedback="true" :show-label="true" :show-require-mark="false" :rules="rules" require-mark-placement="right">

    <n-form-item label="inputNumber" path="undefined">
      <n-input-number :clearable="false" :step="1" size="small" :show-button="true" />
    </n-form-item>
    <n-form-item label="select" path="undefined">
      <n-select size="small" placeholder="请选择" :multiple="false" :clearable="true"
        :options="[{ label: '1', value: '' }, { label: '2', value: '' }, { label: '3', value: '' }]" />
    </n-form-item>
    <n-form-item label="input" path="undefined">
      <n-input :clearable="false" type="text" size="medium" />
    </n-form-item>
    <n-form-item label="radio" path="undefined">
      <n-radio-group size="medium">
        <n-space>

        </n-space>
      </n-radio-group>
    </n-form-item>

    <n-form-item>
      <n-space justify="center">
        <n-button @click="handleValidateClick">确认</n-button>
        <n-button>取消</n-button>
      </n-space>
    </n-form-item>
  </n-form>
</template>
  
<script setup type="ts">
import { NInputNumber, NSelect, NInput, NRadio, NRadioGroup, NSpace, NButton, NForm, NFormItem } from 'naive-ui';
function handleValidateClick () {
  console.log("hello")
}
</script>
