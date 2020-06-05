<template>

  <b-container>
    <b-row>
      <b-col>
        <input
          type="text"
          v-model="height"
          size="5"
        > Height
        <input type="range" class="custom-range range-small" v-model="height"/>
      </b-col>
      <b-col>
        <input
          type="text"
          v-model="width"
          size="5"
        > Width
        <input type="range" class="custom-range range-small" v-model="width"/>
      </b-col>
    </b-row>

    <b-row>
      <b-col>
        <spire-gif
          :height="newSettings.height"
          :width="newSettings.width"
          :setup="newSettings.setup"
          :time-str="timeStr"
        />
      </b-col>
      <b-col>
        <b-button @click="refreshGif()">REFRESH</b-button><br/>
        <b-button @click="setupToObj()">JSON to UI</b-button>
        <b-button @click="refreshGif()">UI to JSON</b-button>
        <b-button @click="formatJson()">Format JSON</b-button>
      </b-col>
    </b-row>
    <b-row>
      <b-col v-for="(spire, index) in setupObj.spires" :key="spire.spire_height[0]">
        <spire-control :spire="spire" :index="index" @update-spire="updateSpire"></spire-control>
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
import SpireControl from '~/components/SpireControl.vue'

export default {
  components: {
    SpireGif,
    SpireControl
  },
  data() {
    return {
      apiUrl: process.env.apiUrl,
      height: 100,
      width: 100,
      setup: `{"flash_0": 15,"flash_1": 25,"functions": [{"name": "s1", "function": "sin", "frequency": 1, "phase": 0}, {"name": "s2", "function": "sin", "frequency": 2, "phase": 0}, {"name": "s3", "function": "sin", "frequency": 3, "phase": 0}], "spires": [{"base_wiggle": [0, "s3", null], "spire_base_width": [0.3, null, null], "spire_base_center": [0.75, null, null], "spire_height": [0.75, "s2", null]}, {"base_wiggle": [0, null, null], "spire_base_width": [0.3, null, null], "spire_base_center": [0.25, null, null], "spire_height": [0.5, "s1", null]}]}`,
      setupObj: {},
      newSettings: {
        height: this.height,
        width: this.width,
        setup: this.setup
      },
      timeStr: new Date().getTime().toString()
    };
  },
  methods: {
    refreshGif: function() {
      this.newSettings.height = parseInt(this.height);
      this.newSettings.width = parseInt(this.width);
      this.newSettings.setup = this.setup;
      this.timeStr = new Date().getTime().toString();
    },
    setupToObj: function() {
      this.setupObj = JSON.parse(this.setup);
    },
    setupToStr: function() {
      this.setup = JSON.stringify(this.setupObj);
    },
    formatJson: function() {
      this.setup = JSON.stringify(JSON.parse(this.setup), null, 4);
    },
    updateSpire: function(e) {
      this.setupObj.spires[e.index] = e;
      this.setupToStr();
      this.formatJson();
    }
  },
  mounted() {
    this.setupToObj();
    this.formatJson();
  }
}
</script>

<style>
.range-small {
    width: 5rem;
}
.container {
  margin: 0;
}
</style>
