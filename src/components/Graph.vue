<!--VueJS component that displays data in a graph, has a title and some text to show the current data value, the average, and the maximum value. Script needs to be written in typescript-->
<script setup lang="ts">
import Chart from "chart.js/auto";
import {onMounted, ref} from 'vue';

var graphData = [
]

//generate unique id for the canvas element
function makeid(length: number) {
  var result = "";
  var characters = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
  var charactersLength = characters.length;
  for (var i = 0; i < length; i++) {
    result += characters.charAt(Math.floor(Math.random() *
      charactersLength));
  }
  return result;
}
let id = makeid(10);

//Define the props
const props = defineProps(
  {
    title: String,
    units: String,
    ylabel: String,
    xlabel: String
  }
);

//Function that gets called from the parent to update the graph
function updateGraph(data: number) {
  //Update the graph
  graphData.push({time: graphData.length, value: data});

  //Update the graph
  chart.value?.data.labels.push(graphData.length.toString());
  chart.value?.data.datasets[0].data.push(data);

  //Update the current value
  document.getElementById("value-current")!.innerHTML = data.toString();

  //Update the average value
  let average = 0;
  for (let i = 0; i < graphData.length; i++) {
    average += graphData[i].value;
  }
  average /= graphData.length;
  document.getElementById("value-average")!.innerHTML = average.toString();

  //Update the maximum value
  let max = 0;
  for (let i = 0; i < graphData.length; i++) {
    if (graphData[i].value > max) {
      max = graphData[i].value;
    }
  }
  document.getElementById("value-max")!.innerHTML = max.toString();
}

//Create a test line chart using chart.js.

const chart = ref<Chart>();

onMounted(() => {
  const ctx = document.getElementById(id) as HTMLCanvasElement;
  chart.value = new Chart(ctx, {
    type: "line",
    data: {
      labels: [],
      datasets: [
        {
          label: props.ylabel,
          data: graphData.map((d) => d.value),
          borderColor: "rgb(255, 99, 132)",
          backgroundColor: "rgba(255, 99, 132, 0.5)",
          tension: 0.1,
        },
      ],
    },
    options: {
      //Disable animations
      animation: false,
      responsive: true,

      scales: {
        y: {
          beginAtZero: true,
        },
      },
    },
  });
});
</script>

<template>
  <div class="telem-graph">
    <h3>Title</h3>
    <h5>Units</h5>
    <hr>
    <p>
      Current: <span id="value-current">0</span><br>
      Average: <span id="value-average">0</span><br>
      Maximum: <span id="value-max">0</span><br>
    </p>
    <div class="graph">
      <canvas id="{{ id }}"></canvas>
    </div>
  </div>
</template>

<style scoped>
@import url("../style.css");
.telem-graph {
  background-color: #6664;
  border: 1px solid var(--color-accent);
  padding: 5px;
  border-radius: 5px;
  /* max-width: 500px; */
}

.graph {
  width: 100%;
  height: 200px;
}
.graph canvas {
  width: 100%;
  height: 100%;
}
</style>