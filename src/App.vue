<script setup>
import 'mind-ar/dist/mindar-image.prod.js'
import 'aframe'
import 'aframe-extras'
import 'mind-ar/dist/mindar-image-aframe.prod.js'
import MindarViewer from './components/MindarViewer.vue'

</script>

<template>
  <div class="mindar-container">
    <mindar-viewer />
  </div>
</template>
