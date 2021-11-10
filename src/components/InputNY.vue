boolean input with text that acts like a radio input
example:
<!--
  <InputNY v-model="optionBoolean">
    option text
  </InputNY>
-->

<template>
  <div class="container">
    <span><slot></slot></span>
    
    <input type="radio" :name="this.uuid" :id="this.uuid + '-1'" value="false" v-model="modelValueAsString">
    <label :for="this.uuid + '-1'">no</label>

    <input type="radio" :name="this.uuid" :id="this.uuid + '-2'" value="true" v-model="modelValueAsString">
    <label :for="this.uuid + '-2'">yes</label>
  </div>
</template>

<script>
let uuid = 0;

export default {
  name: 'InputNY',
  props: {
    modelValue: {
      type: Boolean,
      required: true,
    },
  },
  emits: ['update:modelValue'],
  computed: {
    // typecasts the Boolean to a String and back to ensure it pays nice with the radio input
    modelValueAsString: {
      get() {
        return this.modelValue.toString();
      },
      set(newValue) {
        this.$emit('update:modelValue', newValue === "true");
      },
    },
  },
  // create unique id
  beforeCreate() {
    this.uuid = "inputny-" + uuid.toString();
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
</style>