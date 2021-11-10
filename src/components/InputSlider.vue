number input with text and a slider
example:
<!--
  <InputSlider v-model="optionNumber">
    option text
  </InputSlider>
-->

<template>
  <div class="container">
    <span :for="this.uuid"><slot></slot></span>
    
    <input class="input-slider" type="range" :id="this.uuid + 'slider'" min="0" max="30"
      :value="modelValue" @input="$emit('update:modelValue', $event.target.value)">
    <input class="input-box" type="number" :id="this.uuid" min="0"
      :value="modelValue" @input="$emit('update:modelValue', $event.target.value)">
  </div>
</template>

<script>
let uuid = 0;

export default {
  name: 'InputSlider',
  props: {
    modelValue: {
      type: Number,
      required: true,
    },
  },
  emits: ['update:modelValue'],
  // create unique id
  beforeCreate() {
    this.uuid = "inputslider-" + uuid.toString();
    uuid += 1;
  },
}
</script>

<style scoped>
.container {
  display: flex;
  Padding: 10px 20px 10px 10px;
}
span {
  flex-grow: 1;
}
.input-box {
  padding: 8px 10px;
  border: 1px solid #A4A4A4;
  box-sizing: border-box;
  border-radius: 3px;
  width: 98px;
}
</style>