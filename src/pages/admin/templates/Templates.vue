<template>
    <va-content class="typography content">
       
        <h1>
            {{ t('menu.templates') }}
        </h1>
        <Iotindicator></Iotindicator>
        <va-button @click="templates.methods.cambiar">Send</va-button>
        
    </va-content>
    
</template>
<script setup lang="ts">
//el export que debe de estar aqui se busca y se encuentra en index.ts
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
import Iotindicator from '../../../components/navbar/components/Widgets/Iotindicator.vue'
import templates from './templates'
/*function cambiar() {
    console.log("cambiar");
}*/

const { t } = useI18n()


/*

const options = ref([
    { label: 'One', value: 'one' },
    { label: 'Two', value: 'two' },
    { label: 'Three', value: 'three' },
])*/
const model = ref('three')
const activePage = ref(4)
/*function cambiar() {
    console.log("cambiar");
    this.$nuxt.$emit('widget-topic')
}*/
</script>
<style lang="scss" scoped>
.text--secondary {
    color: var(--va-secondary);
}
</style>