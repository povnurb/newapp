<template>
    <va-card class="flex " :class="[config.column]">
        <va-card-title>
            <h3 class="card-title">{{ config.selectedDevice.name }} - {{config.variableFullName}}</h3>
        </va-card-title>
        <va-icon class="mr-3 mb-3 ml-4 fa-4x fa " :class="[config.icon]" :style="{color: getIconColorClass()}" size="40px"></va-icon>
    </va-card>
</template>


<script>
export default {
    //props: ['config'],
    data() {
        return {
            value: false,
            config: {
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
            }
        }
    },
    onMounted() {
        //this.$on('widget-topic',this.processReceivedData)
        //this.$nuxt.$on('widget-topic',this.processReceivedData)
        const topic = this.config.userId + "/" + this.config.selectedDevice.dId + "/" + this.config.variable + "/sdata" 
        console.log(topic);
        //this.$on(topic, this.processReceivedData)
    },
    methods: {

        processReceivedData(data) {
            console.log("received");
            console.log(data);
            //this.value = data.value;
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
        }
    }
}
</script>