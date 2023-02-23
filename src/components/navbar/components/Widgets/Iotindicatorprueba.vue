<template>
    <va-card class="flex " :class="[config.column]">
        <va-card-title >
            <h3 class="card-title" >{{config.selectedDevice.name}} - {{config.variableFullName}}</h3>
            
        </va-card-title>
        <div class="va-text-center">
        <va-icon class="mr-3 mb-3 ml-4 fa-4x fa " :class="[config.icon]" :style="{ color: getIconColorClass() }" size="40px"></va-icon>
        </div>
    </va-card>
</template>


<script lang="ts">

import useEmitter from '../../../../../plugin/useEmitter'
import { property } from 'lodash'
import {ref} from 'vue'
import data from './Iotindicator.vue'
import { videoOverlay } from 'leaflet';
import viteConfig from '../../../../../vite.config';
export default {
    props: ['config'],
    data() {
        return {
            value:false,
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
                class: 'warning'
            }*/
        }
    },
    mounted(){
        
        const topic = this.config.userId + "/" + this.config.selectedDevice.dId + "/" + this.config.variable + "/sdata" 
        console.log(topic);
        useEmitter.$on(topic, this.processReceivedData)
    },
    methods: {
        sendData() {
            this.value = !this.value;
            const toSend = {
                value: this.value
            }
            useEmitter.$emit('widget-topic', toSend)
        },
            
        processReceivedData(data) {
            //console.log("received");
            //console.log(data);
            this.value = data.value
        },

        getIconColorClass() {
            if (!this.value) {
                //console.log(data.value)
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

        
        },
        cambiar(valor: string) {
            if (valor=="true") { 
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
            /*property.value = data.value;*/
            
        }
        
    }
}
</script>