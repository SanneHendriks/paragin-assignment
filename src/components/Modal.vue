modal with a close button to wrap content
example:
<!--
  <Modal v-model="modalStateBoolean">
    <template v-slot:title>Title text</template>
    <template v-slot:default>
      <Content/>
    </template>
  </Modal>
-->

<template>
  <div v-if="modelValue" class="container">
    <h3>
      <slot name="title"></slot>
      <button @click="$emit('update:modelValue', false)">X</button>
    </h3>
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    modelValue: {
      type: Boolean,
      required: true,
    },
  },
  emits: ['update:modelValue'],
}
</script>

<style scoped>
.container {
  padding: 8px;
  background: #5BA012;
  max-width: 960px;
  min-width: 600px;
  box-sizing: border-box;
}
.content {
  background: #FFFFFF;
}
h3 {
  text-align: center;
  position: relative;
  font-weight: 400;
  font-size: 16px;
  color: #FFFFFF;
  margin: 1px 0 9px 0;
}
button {
  background: #CF191E;
  right: 0;
  position: absolute;
  width: 46px;
  height: 20px;
  border: 0;
  color: #FFFFFF;
}
</style>