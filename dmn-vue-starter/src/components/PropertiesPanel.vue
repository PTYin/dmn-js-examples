<template>
  <div id="properties-panel">
    <div class="property-label" v-for="(value, key) in info">{{ `${key}: ${value}` }}</div>
  </div>
</template>

<script>
  export default {
    name: 'PropertiesPanel',
    props: {
      info: {}
    },
    data() {
      return {test: 'abc'}
    }
  }
</script>

<style>
  #properties-panel {
    width: 100%;
    height: 100%;
    background-color: #fff;
    border-color: rgba(0, 0, 0, 0.09);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.09);
    padding: 0;
  }

  .property-label {
    width: 100%;
    padding: 10px 0 0 50px;
  }
</style>