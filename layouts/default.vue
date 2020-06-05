<template>
  <b-container>
    <b-row>
      <b-col>
        <doom-header />
      </b-col>
    </b-row>
    
    <b-row>
      <b-col>
        <nuxt />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import DoomHeader from '~/components/DoomHeader.vue'

export default {
  components: {
    DoomHeader
  }
}
</script>

<style>
body {
  background-color: rgb(4, 207, 173);
}
</style>
