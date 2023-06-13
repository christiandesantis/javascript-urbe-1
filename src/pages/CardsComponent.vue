<template>
  <div>
    <form @submit.prevent="agregarAlumno">
      <input type="text" v-model="nuevoAlumno.cedula" placeholder="Cédula">
      <input type="text" v-model="nuevoAlumno.nombre" placeholder="Nombre">
      <input type="number" v-model="nuevoAlumno.notaMatematicas" placeholder="Nota de Matemáticas">
      <input type="number" v-model="nuevoAlumno.notaFisica" placeholder="Nota de Física">
      <input type="number" v-model="nuevoAlumno.notaProgramacion" placeholder="Nota de Programación">
      <button type="submit">Agregar Alumno</button>
    </form>

    <div>
      <h5>Promedios:</h5>
      <p>Promedio de Matemáticas: {{ promedioMatematicas }}</p>
      <p>Promedio de Física: {{ promedioFisica }}</p>
      <p>Promedio de Programación: {{ promedioProgramacion }}</p>
      <p>Número de alumnos aprobados en Matemáticas: {{ numAprobadosMatematicas }}</p>
      <p>Número de alumnos aplazados en Matemáticas: {{ numAplazadosMatematicas }}</p>
      <p>Número de alumnos que aprobaron todas las materias: {{ numAprobadosTodas }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface Alumno {
  cedula: string;
  nombre: string;
  notaMatematicas: number;
  notaFisica: number;
  notaProgramacion: number;
}

const alumnos = ref<Alumno[]>([])
const nuevoAlumno = ref<Alumno>({
  cedula: '',
  nombre: '',
  notaMatematicas: 0,
  notaFisica: 0,
  notaProgramacion: 0
})

const promedioMatematicas = ref(0)
const promedioFisica = ref(0)
const promedioProgramacion = ref(0)
const numAprobadosMatematicas = ref(0)
const numAplazadosMatematicas = ref(0)
const numAprobadosTodas = ref(0)

const agregarAlumno = () => {
  alumnos.value.push({ ...nuevoAlumno.value })
  nuevoAlumno.value = {
    cedula: '',
    nombre: '',
    notaMatematicas: 0,
    notaFisica: 0,
    notaProgramacion: 0
  }
  calcularPromedios()
}

const calcularPromedios = () => {
  let sumaMatematicas = 0
  let sumaFisica = 0
  let sumaProgramacion = 0
  let numAprobadosMatematicas = 0
  let numAplazadosMatematicas = 0
  let numAprobadosTodas = 0
  let numAprobadosUnaMateria = 0
  let numAprobadosDosMaterias = 0

  for (const alumno of alumnos.value) {
    sumaMatematicas += alumno.notaMatematicas
    sumaFisica += alumno.notaFisica
    sumaProgramacion += alumno.notaProgramacion

    if (alumno.notaMatematicas >= 10) {
      numAprobadosMatematicas++
    } else {
      numAplazadosMatematicas++
    }

    if (
      alumno.notaMatematicas >= 10 &&
      alumno.notaFisica >= 10 &&
      alumno.notaProgramacion >= 10
    ) {
      numAprobadosTodas++
    }

    const numAprobadas =
      (alumno.notaMatematicas >= 10 ? 1 : 0) +
      (alumno.notaFisica >= 10 ? 1 : 0) +
      (alumno.notaProgramacion >= 10 ? 1 : 0)

    if (numAprobadas === 1) {
      numAprobadosUnaMateria++
    } else if (numAprobadas === 2) {
      numAprobadosDosMaterias++
    }
  }

  promedioMatematicas.value =
    sumaMatematicas / (alumnos.value.length || 1)
  promedioFisica.value = sumaFisica / (alumnos.value.length || 1)
  promedioProgramacion.value =
    sumaProgramacion / (alumnos.value.length || 1)
}
</script>
