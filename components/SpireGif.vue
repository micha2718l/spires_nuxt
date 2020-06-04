<template>
    <div>
        <img :src="gifUrl"/>
    </div>
</template>

<script>
export default {
    props: {
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
        }
    },
    data() {
        return {
            gifUrl: this.apiUrl + 'spire_dance_custom.gif' +
            '?width=' + this.width.toString() +
            '&height=' + this.height.toString()
        };
    }
};
</script>

<style>

</style>
