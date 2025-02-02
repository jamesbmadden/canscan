<script setup>
import SectionFrame from '../components/SectionFrame.vue'
import AppButton from '../components/AppButton.vue'
import CameraIcon from 'vue-material-design-icons/Camera.vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// check if the euser has granted camera permission. If they have, go right to the camera page
const checkCameraPermission = async () => {
  const permission = await navigator.permissions.query({ name: "camera" })
  if (permission.state == 'granted') {
    console.log('permission granted')
    router.push('/camera')
  }
}

checkCameraPermission()

const requestCameraPermission = async () => {
  const cameraStream = await navigator.mediaDevices.getUserMedia({video: true})
  // stop the stream, we should now have permissions
  cameraStream.getTracks().forEach(track => track.stop())
  router.push('/camera')
}
</script>

<template>
  <main class="splash-view">
    <SectionFrame colour="#FFEFEF" gap="32px">

      <CameraIcon fillColor="#DD6868" :size="196"></CameraIcon>

      <h1 class="title">Welcome to CanScan!</h1>
      <p class="body">Thank you for supporting Canadian products! To get started, please allow this app to access your camera.</p>

      <AppButton label="Enable Camera" @click="requestCameraPermission"></AppButton>

      <!-- bottom splash text -->
      <p class="body bottom-note">Made with ❤︎ in Montréal, QC</p>
    </SectionFrame>
  </main>
</template>

<style scoped>
.splash-view {
  color: #DD6868;
  height: 100vh;
  text-align: center;
}
.bottom-note {
  position: absolute;
  bottom: 16px;
}
</style>