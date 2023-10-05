<script setup lang="ts">

import Chart from "chart.js/auto";
import {ref} from 'vue';

const chartref = ref('chart');

const testdata = [
  {year: 2010, value: 10}
]

let chart = new Chart(null, {
  type: 'line',
  data: {
    labels: testdata.map(row => row.year),
    datasets: [

    ]
  }
});

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
      <div class="telem-chart">
        <h4>Title</h4>
        <hr>
        <p>
          Current value: 0<br>
          Maximum value: 0<br>
          Average value: 0<br>
        </p>

        <canvas ref="chart">

        </canvas>
      </div>
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
  grid-template-columns: auto auto auto auto auto;
  padding: 10px;
}

/**Telemetry charts */
div.telem-chart {
  background-color: #6664;
  border: 1px solid var(--color-accent);
  padding: 5px;
  border-radius: 5px;
}
</style>
