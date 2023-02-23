<template>
    <va-content class="typography content">
       
        <h1>
            {{ t('menu.templates') }}
        </h1>
        <div class="row">
        <Iotindicator :config="configindicator"></Iotindicator>
        
        </div>
        
    </va-content>
    <va-content class="typography content">
       
            <div class="row" >
            <Iotbutton :config="configButton"></Iotbutton>
            <Iottogglebutton :config="configtoggle"></Iottogglebutton>
            </div>
           
        </va-content>
    
</template>
<script setup lang="ts">
import { extraColors } from '../../../pages/admin/ui/colors/color-presentation/colorsData'
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
import Iotindicator from '../../../components/navbar/components/Widgets/Iotindicator.vue'
import Iotbutton from '../../../components/navbar/components/Widgets/Iotbutton.vue'
import Iottogglebutton from '../../../components/navbar/components/Widgets/Iottogglebutton.vue'
const { t } = useI18n()

const options = ref([
    { label: 'Apagar', value: "false" },
    { label: 'Encender', value: "true" },
    
])


const model = ref("false")

</script>
<script lang="ts">
import useEmitter from '../../../../plugin/useEmitter'
export default {
    data() {
        return {
            value: false,
            configButton: {
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
                class: "#ed34b8", //success,danger,warning,info,secondary,
                //#36e9f6, #ed34b8(violeta),#8f4ed6(purpura), #d40d52(ruby),#ff842b(naranja),
                //#1b9a7c(dark green),#d3ff00(toxic),#81513e(brow)
                message: "{'fanstatus':'stop'}"
            },
            configindicator: {
                userId: "userid",
                selectedDevice: {
                    name: "home",
                    dId: "8888",
                    templateName: "Power Sensor",
                    templateId: "28934750238957",
                    saverRule: true,
                },
                variableFullName: "bomba",
                variable: "var1",
                icon: "fa-lightbulb",
                column: "xs6 md2",
                widget: "indicator",
                class: "warning"
            },
            configtoggle: {
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
            }
        };
    },
    methods: {},
    components: { Iotbutton }
}
</script>
<style lang="scss" scoped>
.text--secondary {
    color: var(--va-secondary);
}

</style>