<template>
    <va-content class="typography content">
       
        <h1>
            {{ t('menu.templates') }}
        </h1>
        <div class="row">
        <Iotindicator :config="config1"></Iotindicator>
        <Iotindicator :config="config2"></Iotindicator>
        </div>
        <div class="flex xs12 lg6">
                    <va-button-toggle
                      v-model="model"
                      preset="outline"
                      :options="options"
                      border-color="info"
                      color="info"
                      @click="Iotindicator.methods?.cambiar(model)"
                    />
                    <va-button-toggle
                          v-model="model2"
                          preset="outline"
                          :options="options2"
                          border-color="info"
                          color="info"
                          @click="cambiar(model2)"
                        />
                    <!--<va-button @click=Iotindicator.methods?.sendData()>{{ t ('buttons.buttonToggles') }}</va-button>-->
                  </div>
        
    </va-content>
    
</template>
<script setup lang="ts">

import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
import Iotindicator from '../../../components/navbar/components/Widgets/Iotindicator.vue'


const { t } = useI18n()




const options = ref([
    { label: 'Apagar', value: "false" },
    { label: 'Encender', value: "true" },
    
])
const options2 = ref([
    { label: 'Apagar', value: "false" },
    { label: 'Encender', value: "true" },

])

const model = ref("false")
const model2 = ref("false")
</script>
<script lang="ts">
import useEmitter from '../../../../plugin/useEmitter'
export default {
    data() {
        return {
            value: false,
            config1: {
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
            },
            config2: {
                userId: 'userid',
                selectedDevice: {
                    name: "home",
                    dId: "8888",
                    templateName: "Power Sensor",
                    templateId: "28934750238957",
                    saverRule: true,
                },
                variableFullName: "led",
                variable: 'var2',
                icon: "fa-lightbulb",
                column: 'xs6 md2', //xs8 md3, xs4 md9, xs3 md4, xs6 md4, xs6 md2
                widget: 'indicator',
                class: 'danger'
            }
        }
    },
    methods: {
        cambiar(valor: string) {
            if (valor == "true") {
                this.value = true;
                const toSend = {
                    value: this.value
                }
                useEmitter.$emit('userid/8888/var2/sdata', toSend)
            } else {
                this.value = false;
                const toSend = {
                    value: this.value
                }
                useEmitter.$emit('userid/8888/var2/sdata', toSend)
            }
            //return data.value
            /*property.value = data.value;*/

        }
    }
}
</script>
<style lang="scss" scoped>
.text--secondary {
    color: var(--va-secondary);
}
</style>