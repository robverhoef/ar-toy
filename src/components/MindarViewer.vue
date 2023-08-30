<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const sceneRef = ref(null)
defineExpose({ sceneRef })
function onArError(event) {
  console.error('AR Error', event)
}
function onArReady() {
  console.debug('AR ready')
}
onMounted(() => {
  sceneRef.value.addEventListener('arError', onArError)
  sceneRef.value.addEventListener('arReady', onArReady)
})
onBeforeUnmount(() => {
  sceneRef.value.removeEventListener('arError', onArError)
  sceneRef.value.addEventListener('arReady', onArReady)
})
</script>
<template>
  <a-scene ref="sceneRef" mindar-image="imageTargetSrc: /arcard.mind;" color-space="sRGB"
    renderer="colorManagement: true,physicallyCorrectLights" vr-mode-ui="enabled: false"
    device-orientation-permission-ui="enabled: false">
    <a-assets>
      <img id="card" src="/arcard.png" />
      <a-asset-item id="avatarModel" src="/enl_smurf.gltf"></a-asset-item>
    </a-assets>

    <a-camera position="0 0 0" look-controls="enabled: false"></a-camera>

    <a-entity mindar-image-target="targetIndex: 0" animation-mixer="clip: *;">
      <a-plane src="#card" position="-0.2 0.1 0" height="1" width="1" rotation="0 0 0"></a-plane>
      <a-gltf-model rotation="90 0 0 " position="0 0 0" scale="1 1 1" src="#avatarModel"
        animation="property: position; to: 0 0 0; dur: 1000; easing: easeInOutQuad; loop: true; dir: alternate" />
    </a-entity>
  </a-scene>
</template>
