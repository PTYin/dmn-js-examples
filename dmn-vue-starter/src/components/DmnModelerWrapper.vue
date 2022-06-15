<template>
  <div id="canvas"/>
  <div id="js-properties-panel" style="height: 100%">
    <PropertiesPanel v-bind:info="properties"/>
  </div>
</template>

<script>
import DmnModeler from 'dmn-js/dist/dmn-modeler.development'
import PropertiesPanel from "./PropertiesPanel.vue";
const dishDecision = import.meta.glob('@/assets/dish-decision.dmn', { as: 'raw' })['../assets/dish-decision.dmn']
export default {
  name: 'DmnModelerWrapper',
  components: {PropertiesPanel},
  data() {
    return {
      properties: {}
    }
  },
  async mounted() {
    const modeler = new DmnModeler({
      container: '#canvas',
      height: '100%',
      width: '100%',
      keyboard: {
        bindTo: window
      },
      propertiesPanel: {
        parent: "#js-properties-panel",
      },
    })
    await modeler.importXML(dishDecision);
    const eventBus = modeler.getActiveViewer().get('eventBus')
    eventBus.on('element.click', e => {
      console.log(e)
      const {element} = e
      this.properties.id = element.id
      this.properties.name = element.businessObject.name
      this.properties.type = element.type
      console.log(this.properties)
    })
  }
}
</script>

<style>
@import "dmn-js/dist/assets/diagram-js.css";
@import "dmn-js/dist/assets/dmn-js-drd.css";
@import "dmn-js/dist/assets/dmn-js-decision-table.css";
@import "dmn-js/dist/assets/dmn-js-literal-expression.css";
@import "dmn-js/dist/assets/dmn-js-shared.css";
@import "dmn-js/dist/assets/dmn-font/css/dmn.css";

#canvas {
  width: 100%;
  height: 100%;
}

#js-properties-panel {
  position: absolute;
  right: 0;
  top: 0;
  width: 300px;
}
</style>