<template>
  <div class="q-pa-md">
    <div class="row justify-around">
      <div class="col-5" style="min-height: 300px;">
        <div class="text-center" style="height: 30%; background-color: rgb(156, 226, 44);">
          <div>{{ `A < 40kg` }}</div>
          <div class="text-bold">{{ `${(statistics.aMenor40 * 100).toFixed(2)}%` }}</div>
        </div>

        <div class="text-center" style="height: 30%; background-color: red;">
          <div>{{ `40kg < A < 50kg` }}</div>
          <div class="text-bold">{{ `${(statistics.aEntre40y50 * 100).toFixed(2)}%` }}</div>
        </div>

        <div class="text-center" style="height: 20%; background-color: blue;">
          <div>{{ `50kg < A < 60kg` }}</div>
          <div class="text-bold">{{ `${(statistics.aEntre50y60 * 100).toFixed(2)}%` }}</div>
        </div>

        <div class="text-center" style="height: 20%; background-color: green;">
          <div>{{ `60kg <= A` }}</div>
          <div class="text-bold">{{ `${(statistics.aMayor60 * 100).toFixed(2)}%` }}</div>
        </div>

      </div>

      <div class="col-5">
        <q-form>
          <q-input
            filled
            v-model="cantidadAlumnos"
            type="number"
            label="Numero de alumnos"
            hint="Cuantos alumnos se van a agregar?"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Por favor ingresa un numero de alumnos' ]"
          />

          <div class="q-mt-lg" v-for="(alumno, index) in alumnos" :key="index">
            <q-input
              filled
              v-model="alumnoPeso[index]"
              type="number"
              :label="`Peso alumno ${index + 1}`"
              hint="Cuanto pesa el alumno?"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Por favor ingresa el peso del alumno' ]"
            />
          </div>
        </q-form>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref, watch } from 'vue'

interface Alumno {
  peso: number
}

const cantidadAlumnos = ref(0)

const alumnos = computed<Alumno[]>(() => {
  const arr = []
  for (let i = 0; i < cantidadAlumnos.value; i++) {
    arr.push({ peso: 0 })
  }
  return arr
})

const alumnoPeso = ref([])

watch(cantidadAlumnos, (newVal: number, oldVal: number) => {
  if (newVal < oldVal) alumnoPeso.value = alumnoPeso.value.slice(0, newVal)
})

// watch(alumnos.value, () => {
//   alumnoPeso.value = alumnos.value.map(alumno => alumno.peso)
// })

// watch(alumnoPeso.value, () => {
//   alumnos.value = alumnoPeso.value.map(peso => ({ peso }))
// })

const statistics = computed(() => {
  return {
    aMenor40: (alumnoPeso.value.filter(peso => peso < 40).length / alumnoPeso.value.length) ?? 0,
    aEntre40y50: (alumnoPeso.value.filter(peso => peso >= 40 && peso < 50).length / alumnoPeso.value.length) ?? 0,
    aEntre50y60: (alumnoPeso.value.filter(peso => peso >= 50 && peso < 60).length / alumnoPeso.value.length) ?? 0,
    aMayor60: (alumnoPeso.value.filter(peso => peso >= 60).length / alumnoPeso.value.length) ?? 0
  }
})

</script>
