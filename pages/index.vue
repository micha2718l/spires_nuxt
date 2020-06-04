<template>

  <b-container>
    <b-row>
      <b-col>
        <input
          type="number"
          v-model="height"
        > Height
        <input type="range" class="custom-range" v-model="height"/>
      </b-col>
      <b-col>
        <input
          type="number"
          v-model="width"
        > Width
        <input type="range" class="custom-range" v-model="width"/>
      </b-col>
    </b-row>

    <b-row>
      <b-col>
        <spire-gif
        :height="newSettings.height"
        :width="newSettings.width"
        :setup="newSettings.setup"
        />
      </b-col>
      <b-col>
        <b-button @click="refreshGif()">REFRESH</b-button>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <textarea class="form-control" v-model="setup" rows="15"></textarea>
      </b-col>
    </b-row>
  </b-container>

</template>

<script>
import SpireGif from '~/components/SpireGif.vue'

export default {
  components: {
    SpireGif
  },
  data() {
    return {
      apiUrl: process.env.apiUrl,
      height: 50,
      width: 50,
      setup: `{"functions": [{"name": "s1", "function": "sin", "frequency": 1, "phase": 0}, {"name": "s2", "function": "sin", "frequency": 2, "phase": 0}, {"name": "s3", "function": "sin", "frequency": 3, "phase": 0}], "spires": [{"base_wiggle": [0, "s3", null], "spire_base_width": [0.3, null, null], "spire_base_center": [0.75, null, null], "spire_height": [0.75, "s2", null]}, {"base_wiggle": [0, null, null], "spire_base_width": [0.3, null, null], "spire_base_center": [0.25, null, null], "spire_height": [0.5, "s1", null]}]}`,
      newSettings: {
        height: this.height,
        width: this.width,
        setup: this.setup
      }
    };
  },
  methods: {
    refreshGif: function() {
      this.newSettings.height = parseInt(this.height);
      this.newSettings.width = parseInt(this.width);
      this.newSettings.setup = this.setup;
      
      console.log(this.newSettings);
    }
  }
}
</script>

<style>

</style>
