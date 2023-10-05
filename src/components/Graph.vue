<!--VueJS component that displays data in a graph, has a title and some text to show the current data value, the average, and the maximum value-->

<script setup lang="ts">
const props = defineProps(['title'])
</script>

<template>
    <div>
        <h3>Title</h3>
        <hr>
        <p><h3>Current value: </h3>
        <h3>Max value: </h3>
            Current value: <br>
            Average: <br>
            Maximum: <br>
        </p>
    </div>
</template>

<style scoped>
</style>