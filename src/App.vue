<script setup lang="ts">

import Graph from './components/Graph.vue';

import {onMounted} from 'vue'
</script>

<template>
  <div class="main">
    <div class="toolbar">
      <div class="tb-section">
        <span class="tb-button">Start/Stop</span>
        <span class="tb-button">Clear</span>
        <span class="tb-button">Settings</span>
      </div>
      <div class="tb-section">
        <span class="tb-detail">
          Connection: DISCONNECTED<br>
          Port: /dev/ttyACM0
        </span>
      </div>
    </div>
    <div class="content-grid">
      <Graph cid="test"/>
      <Graph cid="test2"/>
      <Graph cid="test3"/>
      <Graph cid="test4"/>
    </div>
  </div>
</template>

<style scoped>
@import url("./style.css"); /**Import variables */

div.toolbar {
  background-color: #444;
  display: grid;
  grid-template-columns: auto auto auto;
  width: 100%;
  height: fit-content;
}

div.tb-section {
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 5px;

  height: fit-content;
  padding: 5px;
}

span.tb-detail {
  font-size: 10pt;
}

span.tb-button {
  display: block;
  padding: 5px;
  font-size: 14pt;
  background-color: var(--color-primary);
  border: 1px solid var(--color-accent);
  border-radius: 5px;
  transition-property: background-color, color;
  transition-duration: 100ms;
}

span.tb-button:hover {
  background-color: var(--color-accent);
  color: #000;  
}

div.content-grid {
  display: grid;
  grid-template-columns: auto auto auto;
  padding: 10px;
  gap: 5px;
}

/**Telemetry charts */
div.telem-chart {
  background-color: #6664;
  border: 1px solid var(--color-accent);
  padding: 5px;
  border-radius: 5px;
  max-width: initial;
}
</style>
