<template>
    <va-card class="flex va-text-center" :class="[config.column]">
        <va-card-title>
            <h3 class="card-title">{{ config.selectedDevice.name }} - {{ config.variableFullName }}</h3>

        </va-card-title>
         
            <div class="flex md6 offset-md1">
                <va-button-toggle
                    v-model="model"
                    preset="outline"
                    :options="options"
                    border-color="info"
                    color="info"
                    @click="cambiar(model)"
                />
            
            </div>
    </va-card>
</template>
<script setup lang="ts">
import useEmitter from '../../../../../plugin/useEmitter'

import { ref } from 'vue'
import data from './Iottogglebutton.vue'

const options = ref([
    { label: 'Apagar', value: "false" },
    { label: 'Encender', value: "true" },

])

const model = ref("false")
</script>

<script lang="ts">


export default {
    props: ['config'],
    data() {
        return {
            value: false,
            /*config: {
                userId: 'userid',
                selectedDevice: {
                    name: "home",
                    dId: "8888",
                    templateName: "Power Sensor",
                    templateId: "28934750238957",
                    saverRule: true,
                },
                variableFullName: "bomba",
                variable: 'var1',
                icon: "fa-lightbulb",
                column: 'xs8 md3', //xs8 md3, xs4 md9, xs3 md4, xs6 md4, xs6 md2
                widget: 'indicator',
                class: 'warning'
            }*/
        }
    },
    mounted() {

       
    },
    methods: {
        

        processReceivedData(data) {
          
            this.value = data.value
        },

        getIconColorClass() {
            if (!this.value) {
                
                return "black"

            }
            if (this.config.class == "success") {
                return "green"
            }
            if (this.config.class == "primary") {
                return "blue"
            }
            if (this.config.class == "warning") {
                
                return "yellow"
            }
            if (this.config.class == "danger") {
                return "brown"
            }
            if (this.config.class == "secondary") {
                return "brown"
            } else {
                return this.config.class
            }

        },
        cambiar(valor: string) {
            if (valor == "true") {
                this.value = true;
                const toSend = {
                    value: this.value
                }
                useEmitter.$emit('userid/8888/var1/sdata', toSend)
            } else {
                this.value = false;
                const toSend = {
                    value: this.value
                }
                useEmitter.$emit('userid/8888/var1/sdata', toSend)
            }
            return data.value
           

        }

    }
}
</script>
<style lang="scss" scoped>
.text--secondary {
    color: var(--va-secondary);
}
</style>