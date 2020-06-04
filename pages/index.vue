<template>
  <div class="container">
    <spire-gif
    :height="200"
    :width="200"
    >
    </spire-gif>
  </div>
</template>

<script>
import SpireGif from '~/components/SpireGif.vue'

export default {
  components: {
    SpireGif
  },
  data() {
    return {
      apiUrl: process.env.apiUrl
    };
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
