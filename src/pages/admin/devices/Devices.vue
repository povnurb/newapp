<template>
  <va-content class="typography content">
    <h1>
      {{ t('menu.devices') }}
    </h1>
  </va-content>
  <div class="cards">
    <div class="cards-container row d-flex wrap align--start">
      <template v-for="loop in listLoops" :key="loop + '-0'">
        <div class="flex xs12 sm6 md6 xl6">
          <va-card>
            <va-card-title>
              {{ t('cards.title.withControls') }}
              <va-spacer />
              <va-button class="mr-1" size="small" icon="refresh" />
              <va-button size="small" icon="gear" />
            </va-card-title>
            <va-card-content>{{ t('cards.contentTextLong') }}</va-card-content>
          </va-card>
        </div>

        <div class="flex xs12 sm6 md6 xl6">
          <va-card>
            <va-card-title>
              {{ t('cards.title.withControls') }}
              <va-spacer />
              <va-button class="mr-1" size="small" icon="refresh" />
              <va-button size="small" icon="gear" />
            </va-card-title>
            <va-card-content>{{ t('cards.contentTextLong') }}</va-card-content>
          </va-card>
        </div>

        <div class="flex xs12 sm6 md6 xl6">
          <va-card>
            <va-card-title>
              <va-icon class="mr-3" name="cogs" />
              {{ t('cards.title.customHeader') }}
            
              {{ t('cards.title.withControls') }}
              <va-spacer />
              <va-button class="mr-1" size="small" icon="refresh" />
              <va-button size="small" icon="gear" />
            
            </va-card-title>
            <va-card-content>{{ t('cards.contentTextLong') }}</va-card-content>
          </va-card>
        </div>

        <div class="flex xs12 sm6 md6 xl6">
          <va-card>
            <va-card-content>
              <p>{{ t('cards.title.withoutHeader') }}</p>
              {{ t('cards.contentTextLong') }}
            </va-card-content>
          </va-card>
        </div>

        <div class="flex xs12 sm6 md3 xl3 lg3 xl3">
          <va-card color="success">
            <va-card-content>{{ t('cards.contentTextLong') }}</va-card-content>
          </va-card>
        </div>

        <div class="flex xs12 sm6 md3 xl3 lg3 xl3">
          <va-card color="danger">
            <va-card-content>{{ t('cards.contentTextLong') }}</va-card-content>
          </va-card>
        </div>
      </template>
    </div>

    <va-inner-loading class="justify-center py-3" style="width: 100%" :loading="isLoading">
      <va-button @click="addCards()">
        {{ t('cards.button.showMore') }}
      </va-button>
    </va-inner-loading>
  </div>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  import { useI18n } from 'vue-i18n'
  const { t } = useI18n()

  const listLoops = ref(1)
  const isLoading = ref(false)

  function addCards() {
    isLoading.value = true
    setTimeout(() => {
      isLoading.value = false
      ++listLoops.value
    }, 1000)
  }
</script>

<style lang="scss">
  .cards-container {
    .va-card {
      margin: 0;
    }
  }
</style>
