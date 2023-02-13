<template>
    <va-content class="typography content">
        <h1>
            {{ t('menu.alarms') }}
        </h1>
    </va-content>
</template>
<script setup lang="ts">
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
const { t } = useI18n()

const options = ref([
    { label: 'One', value: 'one' },
    { label: 'Two', value: 'two' },
    { label: 'Three', value: 'three' },
])
const model = ref('three')
const activePage = ref(4)
</script>