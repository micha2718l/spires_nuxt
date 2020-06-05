<template>
    <div>
        Spire #{{ index }}<br/>
        <table class="table">
            <tbody>
                <tr>
                    <td>Base Wiggle [{{ base_wiggle_amount }}]</td>
                    <td>
                        <input type="number" v-model="base_wiggle_amount" />
                        <input type="range" max="2" min="0" step="0.01" @change="update()" v-model="base_wiggle_amount" />
                    </td>
                </tr>
                <tr>
                    <td>Base Width [{{ base_width_amount }}]</td>
                    <td>
                        <input type="number" v-model="base_width_amount" />
                        <input type="range" max="2" min="0" step="0.01" @change="update()" v-model="base_width_amount" />
                    </td>
                </tr>
                <tr>
                    <td>Base Center [{{ base_center_amount }}]</td>
                    <td>
                        <input type="number" v-model="base_center_amount" />
                        <input type="range" max="1" min="0" step="0.01" @change="update()" v-model="base_center_amount" />
                    </td>
                </tr>
                <tr>
                    <td>Height [{{ height_amount }}]</td>
                    <td>
                        <input type="number" v-model="height_amount" />
                        <input type="range" max="2" min="0" step="0.01" @change="update()" v-model="height_amount" />
                    </td>
                </tr>
            </tbody>
        </table>
    </div> 
</template>

<script>
export default {
    props: {
        spire: {
            type: Object,
            required: true
        },
        index: {
            type: Number,
            required: false,
            default: 0
        }
    },
    data() {
        return {
            base_wiggle_amount: this.spire.base_wiggle[0],
            base_width_amount: this.spire.spire_base_width[0],
            base_center_amount: this.spire.spire_base_center[0],
            height_amount: this.spire.spire_height[0],

            base_wiggle_function_0: this.spire.base_wiggle[1],
            base_width_function_0: this.spire.spire_base_width[1],
            base_center_function_0: this.spire.spire_base_center[1],
            height_function_0: this.spire.spire_height[1],

            base_wiggle_function_1: this.spire.base_wiggle[2],
            base_width_function_1: this.spire.spire_base_width[2],
            base_center_function_1: this.spire.spire_base_center[2],
            height_function_1: this.spire.spire_height[2],

        }
    },
    computed: {

    },
    methods: {
        update: function() {
            let updateSpire = {
                base_wiggle: [parseFloat(this.base_wiggle_amount), this.base_wiggle_function_0, this.base_wiggle_function_1],
                spire_base_width: [parseFloat(this.base_width_amount), this.base_width_function_0, this.base_width_function_1],
                spire_base_center: [parseFloat(this.base_center_amount), this.base_center_function_0, this.base_center_function_1],
                spire_height: [parseFloat(this.height_amount), this.height_function_0, this.height_function_1],
                index: this.index
            }
            this.$emit('update-spire', updateSpire);
        }
    }
}
</script>