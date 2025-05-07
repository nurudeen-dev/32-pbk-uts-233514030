<script setup>
import { ref } from 'vue'

const tugas = ref([
  {
    id: 1,
    nama: 'Tugas 1',
    status: 'Belum Selesai',
  },
  {
    id: 2,
    nama: 'Tugas 2',
    status: 'Belum Selesai',
  },
  {
    id: 3,
    nama: 'Tugas 3',
    status: 'Belum Selesai',
  },
])
</script>

<template>
  <div>
    <ul>
      <li v-for="tugas in tugas" :key="tugas.id">
        {{ tugas.nama }} - {{ tugas.status }}
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
