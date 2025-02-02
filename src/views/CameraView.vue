<script setup>
import { useTemplateRef, onMounted, ref } from 'vue'
import SectionFrame from '../components/SectionFrame.vue'

const isScanned = ref(false)

const viewfinder = useTemplateRef('viewfinder')

let cameraStream

// start the video stream and set the video component to use it
// permission should already be granted, but if not, it'll ask anyways
const startVideo = async () => {

  cameraStream = await navigator.mediaDevices.getUserMedia({video: true})

  viewfinder.value.srcObject = cameraStream
  viewfinder.value.play()

}

// pause the video stream and move into the scanned view
const onScan = () => {

  // stop the video
  viewfinder.value.pause()
  // end the stream
  cameraStream.getTracks().forEach(track => track.stop())
  isScanned.value = true

}

// start the video when the template is rendered
onMounted(() => {
  startVideo()
  // temp: click viewfinder to scan
  viewfinder.value.onclick = () => {
    onScan()
  }
})

</script>

<template>
  <div class="camera-header">
    <h1 class="title">CanScan</h1>
  </div>
  <div class="camera-panel-container">
    <video ref="viewfinder" class="viewfinder" :class="isScanned ? 'minimize' : ''"></video>

    <!-- the result of the scan -->
    <SectionFrame v-if="isScanned" colour="#DD6868" gap="16px">
      <p>scan result here</p>
    </SectionFrame>
  </div>
</template>

<style scoped>
.camera-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 256px;
  /* Top fade */
  background: linear-gradient(180deg, #000000 0%, rgba(0, 0, 0, 0) 100%);
}
.title {
  position: absolute;
  text-align: center;
  height: 128px;
  left: 50%;
  transform: translate(-50%);
  top: 0px;

  font-family: 'Roboto';
  font-style: normal;
  font-weight: 900;
  font-size: 48px;
  line-height: 56px;
  display: flex;
  align-items: center;
  text-align: center;

  color: #DD6868;

  /* cool gradient text 
  background: linear-gradient(90deg, #DD6868 0%, #5F0000 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-fill-color: transparent; */
}
.camera-panel-container {
  height: 100vh;
  display: flex;
  flex-direction: column;
}
.viewfinder {
  width: 100%;
  height: 100%;
  border-radius: 64px;
  background: white;
  object-fit: cover;
}
.viewfinder.minimize {
  aspect-ratio: 1 / 1;
  height: auto;
}
</style>
