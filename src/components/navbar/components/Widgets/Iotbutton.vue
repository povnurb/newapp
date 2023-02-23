<template>
    <va-card class="flex " :class="[config.column]">
        <va-card-title>
            <h3 class="card-title">{{ config.selectedDevice.name }} - {{ config.variableFullName }}</h3>

        </va-card-title>
        <div class="va-text-center">
         <va-button @click="sendValue()" :color= "config.class"  :style="{ color: getIconColorClass() }" >Cambiar</va-button>
         <!--<va-button preset="plain" color="danger" >Cambiar</va-button>-->
         </div>
    </va-card>
</template>
<script setup lang="ts">
import useEmitter from '../../../../../plugin/useEmitter'
import { ToastPosition, useToast } from 'vuestic-ui'
import { property } from 'lodash'
import { ref } from 'vue'
import data from './Iotindicator.vue'
import ColorPresentation from '../../../../pages/admin/ui/colors/color-presentation/ColorPresentation.vue'
import { themeColors, extraColors, buttonGradients } from '../../../../pages/admin/ui/colors/color-presentation/colorsData'
import { videoOverlay } from 'leaflet';
import viteConfig from '../../../../../vite.config';


</script>

<script lang="ts">

export default {
    props: ['config'],
    data() {
        return {
            sending: false,
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
                column: 'xs6 md2', //xs8 md3, xs4 md9, xs3 md4, xs6 md4, xs6 md2
                widget: 'indicator',
                class: 'warning',
                message: "{'fanstatus':'stop'}"
            }*/
        };
    },
    mounted() {

        /*const topic = this.config.userId + "/" + this.config.selectedDevice.dId + "/" + this.config.variable + "/sdata"
        console.log(topic);
        useEmitter.$on(topic, this.processReceivedData)*/
    },
    methods: {
        sendValue() {
            
            this.sending = true;
            setTimeout(()=>{
                this.sending = false;
            }, 500);
            const toSend = {
                topic: this.config.userId + "/" + this.config.selectedDevice.dId + "/" + this.config.variable + "/actdata",
                msg: {
                    value: this.config.message
                }
            };
            console.log(toSend);
            useEmitter.$emit('mqtt-sender', toSend);
        },

        /*processReceivedData(data) {
            //console.log("received");
            //console.log(data);
            this.value = data.value
        },*/

        getIconColorClass() {
            if (!this.sending) {
                return "black"

            }
            if (this.config.class == "success") {
                return "green"
            }
            if (this.config.class == "primary") {
                return "blue"
            }
            if (this.config.class == "warning") {
                //console.log(data.value)
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


        }/*,
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
            property.value = data.value;

        }*/

    }
}

</script>
<style lang="scss" scoped>
.text--secondary {
    color: var(--va-secondary);
}
.va-button-dropdown {
    display: inline-block;
  }
</style>