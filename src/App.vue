<template>
  <div id="app">
    <video id="video" :src="videoSrc" ref="video"></video>
    <button>开启视频会议</button>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      cobtraints: {
        audio: true,
        video: true
      },
      videoSrc: ''
    };
  },
  created(){
    this.getMedia();
  },
  methods: {
    getStream(stream){
      this.$refs.video.src = window.URL.createObjectURL(stream);
      // HTMLMediaElement.srcObject = stream;
      // localVideo.srcObject = stream;
      // localStream = stream;
      // this.$nextTick();
      this.$refs.video.play();
    },
    getMedia(){
      navigator.mediaDevices.getUserMedia(this.cobtraints)
        .then(this.getStream)
        .catch(function(e) {
          alert('getUserMedia() error: ' + e.name);
        });
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
