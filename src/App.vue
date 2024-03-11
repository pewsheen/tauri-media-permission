<script setup lang="ts">
import { Ref, ref } from 'vue';

const playback: Ref<HTMLVideoElement | null> = ref(null);

const displayMediaOptions: DisplayMediaStreamOptions = {
  video: true,
  audio: true,
};

async function startCapture() {
  if (!playback.value) {
    return;
  }

  try {
    playback.value.srcObject = await navigator.mediaDevices.getUserMedia(
      displayMediaOptions
    );
    playback.value.srcObject = await navigator.mediaDevices.getDisplayMedia(
      displayMediaOptions
    );
  } catch (err) {
    console.error(err);
  }
}

function stopCapture(_evt: any) {
  if (!playback.value) {
    return;
  }

  const stream = playback.value.srcObject as MediaStream;
  const tracks = stream.getTracks();
  tracks.forEach((track) => track.stop());
  playback.value.srcObject = null;
}
</script>

<template>
  <div class="container">
    <p>
      <button id="start" @click="startCapture">Start Capture</button
      >&nbsp;<button id="stop" @click="stopCapture">Stop Capture</button>
    </p>
    <video id="video" ref="playback" autoplay></video>
  </div>
</template>

<style scoped>
#video {
  border: 1px solid #999;
  width: 98%;
  max-width: 860px;
}

#log {
  width: 25rem;
  height: 15rem;
  border: 1px solid black;
  padding: 0.5rem;
  overflow: scroll;
}
</style>
