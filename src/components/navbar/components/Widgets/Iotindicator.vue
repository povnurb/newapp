<template>
    <va-card class="flex " :class="[config.column]">
        <va-card-title >
            <h3 class="card-title" >{{config.selectedDevice.name}} - {{config.variableFullName}}</h3>
            
        </va-card-title>
        <div class="va-text-center">
        <va-icon class=" fa " :class="[config.icon]" :style="{ color: getIconColorClass() }" size="40px"></va-icon>
        </div>
    </va-card>
</template>


<script lang="ts">

import useEmitter from '../../../../../plugin/useEmitter'

import data from '../../components/Widgets/Iotindicator.vue'

export default {
    props: ['config'],
    data() {
        return {
            value:false,
           
        }
    },
    mounted(){
        
        const topic = this.config.userId + "/" + this.config.selectedDevice.dId + "/" + this.config.variable + "/sdata"
        console.log(topic);
        useEmitter.$on(topic, this.processReceivedData)
    },
    unmounted() {
        const topic = this.config.userId + "/" + this.config.selectedDevice.dId + "/" + this.config.variable + "/sdata"
        //console.log("desescribir")
        useEmitter.$off(topic)
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
            //console.log("received")
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
            
        }
        
    }
}
</script>