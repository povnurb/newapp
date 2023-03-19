<template>
    <va-content class="typography content">
        <h1>
            {{ t('menu.templates') }}
        </h1>
     </va-content>
    <div class="cards-container row d-flex wrap align--start">
        <!--Widget configurator-->
        <div class="flex xs12">
          <va-card>
            <va-card-title>
              Widgets
            </va-card-title>
        
            <va-card-content>
              <form>
                <div class="row">
                    <!--widget Selector and forms-->
                    <div class="flex xs6">    
                        <!--widget selector-->
                        <va-select     
                                v-model="widgetType"
                                placeholder="Select Widget"
                                :label="t('forms.selects.searchable')"
                                searchable
                                :options="simpleOptions"
                          />                                               
                        <br />         
                        <!--Forms number char type-->
                        <!--<div  v-if="simpleOptions[0].value == 'numberchart'">-->
                        <form v-if=" widgetType == 'Number Chart Input'">
                          <br /> 
                          {{ t('gb.graphics') }} <!--poner una clase a los div los inputs para que se separen -->
                          <br /> <br />                           
                          <va-input v-model="ncConfig.variableFullName" :label="t('gb.varname')" type="text" ></va-input>
                          <br /> <br />                          
                          <va-input v-model="ncConfig.unit" :label="t('gb.unit')" type="text"></va-input>
                          <br /> <br />                          
                          <va-input v-model="ncConfig.decimalPlaces" :label="t('gb.decimalplaces')" :min="0" :max="3" type="number"></va-input>
                          <br /> <br /> 
                          <va-input v-model="ncConfig.icon" :label="t('gb.icon')" type="text"/>
                          <br /> <br /> 
                          <va-input v-model="ncConfig.chartTimeAgo" :label="t('gb.backtime')" type="number"></va-input>
                            <br /> <br /> 
                          <va-select v-model="ncConfig.class" :label="t('gb.theme')" type="text" 
                          :options="['success','danger','warning','info','secondary',
          '#36e9f6', '#ed34b8 (violeta)','#8f4ed6 (purpura)', '#d40d52 (ruby)','#ff842b (naranja)',
          '#1b9a7c (dark green)','#d3ff00 (toxic)','#81513e (brow)']"/>
                            <br /> <br /> 
                        </form>
                        <!--Forms toggle button type-->
                        <div v-else-if="widgetType == 'Toggle Button Output'">
                            togglebutton
                          </div>
                        <!--Forms button type-->
                        <div v-else-if="widgetType == 'Button Output'">
                            {{ t('gb.button') }}
                          </div>
                        <!--Forms indicator type-->
                          <div v-else-if="widgetType == 'Indicator Input'">
                            {{ t('gb.indicator') }}
                          </div>
                        <!--Forms switch small type-->
                          <div v-else-if="widgetType == 'Small Switch Output'">
                            {{ t('gb.smallswitch') }}
                          </div>
                        <!--Forms switch type-->
                        <div v-else-if="widgetType == 'Switch Output'">
                            {{ t('gb.switch') }}
                            <br /> <br />                           
                            <va-input :label="t('gb.varname')" type="text" ></va-input>
                            <br /> <br /> 
                            <va-input v-model="iotSwitchConfig.icon" :label="t('gb.icon')" type="text"/>
                            <br /> <br /> 
                            <va-select v-model="iotSwitchConfig.class" :label="t('gb.theme')" type="text" 
                            :options="['success', 'danger', 'warning', 'info', 'secondary',
                              '#36e9f6', '#ed34b8 (violeta)', '#8f4ed6 (purpura)', '#d40d52 (ruby)', '#ff842b (naranja)',
                              '#1b9a7c (dark green)', '#d3ff00 (toxic)', '#81513e (brow)']"/>
                              <br /> <br /> 
                            <va-select v-model="iotSwitchConfig.column" :label="t('gb.sizes')" type="text" 
                              :options="['xs12', 'xs8', 'xs6', 'xs4', 'xs2', 'xs1']"/>
                                <br /> <br />
                          </div>
                    </div>

                    <!--widget Preview-->
                    <div class="flex xs6">        
                          <!--<va-select 
                                placeholder="Select Widget"
                                v-model="widgetType"
                                :label="t('forms.selects.searchable')"
                                searchable
                                text-by="description"
                                track-by="id"
                                :options="simpleOptions"
                            >
                            <template #append>
                          <va-button style="margin-right: 0" small> {{ t('cards.button.addWidget')}} </va-button>
                        </template>
                          </va-select>-->
                        </div>
                    

                </div>
                <!--add widget button-->
                <div class="flex offset-xs10">
                    <va-button> {{ t('cards.button.addWidget') }} </va-button>
                </div>
              </form>
            </va-card-content>
        
          </va-card>

        </div>
        <!--Dashboard preview-->
        <!--Save Template-->
        <div class="flex xs12">
              <va-card>
                <va-card-title>
                  {{ t('cards.button.saveTemplate') }}
                </va-card-title>
        
                <va-card-content>
                  <form>
                    <div class="row">
                        <div class="flex md4 sm6 xs12">
                    <label>{{ t('forms.inputs.templateName') }}</label>:<va-input placeholder="Ex: Home, Hogar, Office" />
                  </div>
                      <div class="flex   xs8">
                        <label>{{ t('forms.inputs.templateDescription') }}</label>:
                          <va-input 
                                placeholder="Select Widget"
                                text-by="description"
                                track-by="id"
                            >
                            <template #append>
                              <va-button style="margin-right: 0" small> {{ t('cards.button.saveTemplate') }} </va-button>
                            </template>
                          </va-input>
                        </div>
                    </div>
                  </form>
                </va-card-content>
        
              </va-card>

        </div>
        <!--Template table-->
        <div class="flex xs12">
              <va-card>
                <va-card-title>
                  {{ t('forms.inputs.templates')}}
                </va-card-title>
                <!--
                <va-card-content>
                  <form>
                    <div class="row">
                      <div class="flex xs12">
                          <va-select 
                                placeholder="Select Widget"
                                v-model="widgetType"
                                :label="t('forms.selects.searchable')"
                                searchable
                                text-by="description"
                                track-by="id"
                                :options="simpleOptions"
                            >
                            <template #append>
                              <va-button style="margin-right: 0" small> {{ t('cards.button.addWidget') }} </va-button>
                            </template>
                          </va-select>
                        </div>
                    </div>
                  </form>
                </va-card-content>
              -->
              </va-card>

        </div>

      </div>
           
       
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
//http://vuestic.dev/en/ui-elements/select
const simpleOptions = ref(['Number Chart Input','Indicator Input','Toggle Button Output','Small Switch Output','Switch Output','Button Output'])

const widgetType = ref('')
const tema = ref('success')
const icon = ref('')
const model = ref("false")

</script>
<script lang="ts">
import useEmitter from '../../../../plugin/useEmitter'
import { Id } from '@amcharts/amcharts5/.internal/core/render/backend/Renderer'
export default {
  data() {
    return {
        widget: [],
        templates: [],
        widgetType: "",
        templateName: "",
        templateDescription:"",
        ncConfig: {
          userId: 'sampleuserid',
          selectedDevice: {
              name: "home",
              dId: "8888",
        },
        variableFullName: "temperature",
        variable: 'varname',
        unit: "Watts",
        class: "#ed34b8", //success,danger,warning,info,secondary,
        //#36e9f6, #ed34b8(violeta),#8f4ed6(purpura), #d40d52(ruby),#ff842b(naranja),
        //#1b9a7c(dark green),#d3ff00(toxic),#81513e(brow)
        column: 'xs6 md2', //xs8 md3, xs4 md9, xs3 md4, xs6 md4, xs6 md2
        decimalPlaces: 2,
        widget: 'numberchart',
        icon: "fa-lightbulb",
        chartTimeAgo: '1566',
        demo: true
      },
        iotIndicatorConfig: {
          userId: "userid",
          selectedDevice: {
            name: "home",
            dId: "8888",
          },
          variableFullName: "temperature",
          variable: "varname",
          class: "warning",
          widget: "indicator",
          icon: "fa-lightbulb",
          column: "xs6 md2",
          
            
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
      },
        iotSwitchConfig: {
          userId: 'userid',
            selectedDevice: {
              name: "home",
              dId: "8888",
          },
          variableFullName: "bomba",
          variable: 'varname',
            class: 'warning',
            widget: 'indicator',
            icon: "fa-lightbulb",
            column: 'xs8 md3' //xs8 md3, xs4 md9, xs3 md4, xs6 md4, xs6 md2  
      },
      iotButtonConfig: {
        userId: 'userid',
        selectedDevice: {
          name: "home",
          dId: "8888",
        },
        variableFullName: "bomba",
        text: "send",
        message:"testing123",
        variable: 'varname',
        class: 'warning',
        widget: 'button',
        icon: "fa-lightbulb",
        column: 'xs8 md3' //xs8 md3, xs4 md9, xs3 md4, xs6 md4, xs6 md2  
      },
      };
    },
  methods: {
    },
  components: { Iotbutton }
}
</script>
<style lang="scss" scoped>
.text--secondary {
    color: var(--va-secondary);
}

</style>