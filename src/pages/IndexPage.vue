<template>
  <q-page class="q-pa-md">
    <div class="row justify-around">
      <q-card class="col-md-8">
        <q-tabs
          v-model="tab"
          dense
          class="text-grey"
          active-color="primary"
          indicator-color="primary"
          align="justify"
          narrow-indicator
          >
          <q-tab name="statistics" icon="bar_chart" label="1) Estadística" />
          <q-tab name="interest" icon="fa-solid fa-coins" label="2) Interés" />
          <q-tab name="cards" icon="fa-solid fa-address-card" label="3) Tarjetas" />
        </q-tabs>

        <q-separator />

        <q-tab-panels keep-alive v-model="tab" animated>
          <q-tab-panel name="statistics">
            <div class="text-h6 q-mb-lg">Estadística</div>
            <StatisticsComponent />
          </q-tab-panel>

          <q-tab-panel name="interest">
            <div class="text-h6 q-mb-lg">Interés</div>
            <InterestComponent />
          </q-tab-panel>

          <q-tab-panel name="cards">
            <div class="text-h6 q-mb-lg">Tarjetas</div>
            <CardsComponent />
          </q-tab-panel>
        </q-tab-panels>
      </q-card>
    </div>

  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import StatisticsComponent from 'src/components/StatisticsComponent.vue'
import InterestComponent from './InterestComponent.vue'
import CardsComponent from './CardsComponent.vue'

const tab = ref('statistics')

</script>
