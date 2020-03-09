<template>
  <cytoscape
    ref="cy"
    :config="config"
    v-on:mousedown="addNode"
    v-on:cxttapstart="updateNode"
  >
    <cy-element
      class="cytospace"
      v-for="def in elements"
      :key="`${def.data.id}`"
      :definition="def"
      v-on:mousedown="deleteNode($event, def.data.id)"
    />
  </cytoscape>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "App",
  data() {
    return {
      config: {
        style: [
          {
            selector: "node",
            style: {
              "background-color": "#666",
              label: "data(id)"
            }
          },
          {
            selector: "edge",
            style: {
              width: 3,
              "line-color": "#ccc",
              "target-arrow-color": "#ccc",
              "target-arrow-shape": "triangle"
            }
          }
        ],
        layout: {
          name: "grid",
          rows: 1
        }
      },
      elements: [
        {
          // node a
          data: { id: "a" }
        },
        {
          // node b
          data: { id: "b" }
        },
        {
          // edge ab
          data: { id: "ab", source: "a", target: "b" }
        }
      ]
    };
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

html {
}

body {
  margin: 0;
  padding: 0;
}

* {
  height: 100%;
}
</style>
