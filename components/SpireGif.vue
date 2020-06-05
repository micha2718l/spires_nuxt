<template>
    <div>
        <img v-show="loaded" :src="gifSrc" @load="loadedGif()"/>
        <div v-show="!loaded">Loading...</div>
    </div>
</template>

<script>
export default {
    props: {
        timeStr: {
            type: String,
            required: false,
            default: '000'
        },
        width: {
            type: Number,
            required: false,
            default: 100
        },
        height: {
            type: Number,
            required: false,
            default: 100
        },
        apiUrl: {
            type: String,
            required: false,
            default: process.env.apiUrl
        },
        setup: {
            type: String,
            required: false,
            default: `{"flash_0": 15,"flash_1": 25,"functions": [{"name": "s1", "function": "sin", "frequency": 1, "phase": 0}, {"name": "s2", "function": "sin", "frequency": 2, "phase": 0}, {"name": "s3", "function": "sin", "frequency": 3, "phase": 0}], "spires": [{"base_wiggle": [0, "s3", null], "spire_base_width": [0.3, null, null], "spire_base_center": [0.75, null, null], "spire_height": [0.75, "s2", null]}, {"base_wiggle": [0, null, null], "spire_base_width": [0.3, null, null], "spire_base_center": [0.25, null, null], "spire_height": [0.5, "s1", null]}]}`
        }
    },
    data() {
        return {
            loaded: false
        }
    },
    methods: {
        loadedGif: function() {
            this.loaded = true;
        }
    },
    computed: {
        gifSrc: function() {
            this.loaded = false;
            return this.apiUrl + 'spire_dance_custom.gif' +
            '?width=' + this.width.toString() +
            '&height=' + this.height.toString() +
            '&setup=' + encodeURI(this.setup) +
            '&cacheBust=' + this.timeStr;
        }
    }
};
</script>

<style>

</style>
