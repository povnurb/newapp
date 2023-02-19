<template>
    <va-content class="typography content">
      <h1>
        {{ t('menu.devices') }}
      </h1>
    </va-content>
  
  <div class="cards-container row d-flex wrap align--start">
    <div class="flex xs12">
      <va-card>
        <va-card-title>
          <va-icon class="mr-3" name="vuestic-iconset-forms" />{{ t('forms.inputs.add') }}
        </va-card-title>
        
        <va-card-content>
          <form>
            <div class="row">
              <div class="flex md4 sm6 xs12">
                <label>{{ t('forms.inputs.name') }}</label>:<va-input placeholder="Ex: Home, Hogar, Office" />
              </div>
              <div class="flex md4 sm6 xs12">
                <label>{{ t('forms.inputs.id') }}</label>:<va-input placeholder="Input With Icon">
                  <template #prepend>
                    <va-icon color="gray" name="fa-solid fa-barcode" />
                  </template>
                </va-input>
              </div>
              <div class="flex md4 sm6 xs12">
                <label>{{ t('buttons.select') }}</label>:
                <div>
                  <va-select v-model="popover.template" class="mb-4" :options="colors"/>
                </div>
              </div>
            </div>
          </form>
        </va-card-content>
        
      </va-card>

    </div>

    <va-inner-loading class="justify-center py-3" style="width: 100%" :loading="isLoading">
      
      <va-button color="danger" >{{ t('buttons.save') }}</va-button>
      
    </va-inner-loading>
    
  </div>

  <div class="markup-tables flex">
  
    <va-card>
      <va-card-title>{{ t('menu.devices') }}</va-card-title>
      <va-card-content>
        <div class="table-wrapper">
          <table class="va-table va-table--striped va-table--hoverable">
            <thead>
              <tr>
                <th>{{ t('forms.inputs.name') }}</th>
                <th>{{ t('forms.inputs.id') }}</th>
                <th>{{ t('forms.inputs.template') }}</th>
                <th> <va-list-label>{{ t('forms.inputs.actions') }}</va-list-label></th>
              </tr>
            </thead>
  
            <tbody>
              
              <tr v-for="user in users" :key="user.dId">
               
                <td>{{ user.name }}</td>
                <td>{{ user.dId }}</td>
                <td>{{ user.templateName }}</td>
                <td>
                  
                  <va-switch size="small" v-model="user.saverRule" @click="updateSaverRuleStatus(user.dId)" />
                  <i class=" mr-4" :class="{'fas fa-database' : user.saverRule, 'fas fa-ban': !user.saverRule }"></i>
                  <va-button class="mr-2 mb-2" preset="outline" border-color="danger" color="danger" @click="deleteDevice(user.dId)">
                    {{ t('cards.button.delete') }}</va-button>
                  
                </td>
                
              </tr>
              
            </tbody>
          </table>
        </div>
      </va-card-content>
    </va-card>
  </div>
  <!--<pre>
  {{ data }}</pre>-->
</template>

<script setup lang="ts">

  
  import { ref } from 'vue'
  import { useI18n } from 'vue-i18n'
  import data from './../../../data/tables/markup-table/data.json'
  import { ToastPosition, useToast } from 'vuestic-ui'
  //import ToastPositionPicker from './ToastPositionPicker.vue'

  const { init } = useToast()
  const users = ref(data.slice(0, 8))
  const { t } = useI18n()
  const colors = ref(['success', 'info', 'danger', 'warning', 'gray', 'dark'])
  const listLoops = ref(0)
  const isLoading = ref(false)
  const toastDuration = ref(2500)
  const toastPosition = ref<ToastPosition>('bottom-right')
  const popover = ref({
    title: 'Hey folks!',
    message: 'This tooltip is amazing :D',
    icon: {
      icon: 'print',
      text: 'print',
    },
    template: 'Template',
  })

  function addCards() {
    isLoading.value = true
    setTimeout(() => {
      isLoading.value = false
      ++listLoops.value
    }, 1000)
  }
function getStatusColor(status: string) {
  if (status === 'paid') {
    return 'success'
  }
}
function deleteDevice(dId: string) {
  alert("DELETING" + dId)
}
// funcion que muestra un toast
function launchToast(name: string) {
  init({
    message: "Save Info: " + name,
    position: toastPosition.value,
    duration: Number(toastDuration.value),
  })
}
function launchToast2(name: string) {
  init({
    message: "No Save: " + name,
    position: toastPosition.value,
    duration: Number(toastDuration.value),
    color: "danger"
  })
}
//funcion que busca y compara para mostrar o borrar
function updateSaverRuleStatus(dId: string) {
  var i = 0;
  while (dId != data[i].dId) {
    i++;
  }
  if (data[i].saverRule) {
    launchToast(data[i].name)
    
    data[i].saverRule = false
  } else {
    launchToast2(data[i].name)
    data[i].saverRule = true
  }
}

</script>

<style lang="scss">
.cards-container {
    .va-card {
      margin: 0;
    }
  }
    .markup-tables {
      .table-wrapper {
        overflow: auto;
      }
  
      .va-table {
        width: 100%;
      }
    }
</style>
