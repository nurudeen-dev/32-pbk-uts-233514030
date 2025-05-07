<script setup>
import { ref } from 'vue'

const tugas = ref([
  {
    id: 1,
    nama: 'Tugas 1',
    status: false,
  },
  {
    id: 2,
    nama: 'Tugas 2',
    status: false,
  },
  {
    id: 3,
    nama: 'Tugas 3',
    status: false,
  },
])
const newTugas = ref('')

const tambahTugas = () => {
  if (newTugas.value) {
    tugas.value.push({
      id: tugas.value.length + 1,
      nama: newTugas.value,
      status: false,
    })
    newTugas.value = ''
  }
}

const hapusTugas = (id) => {
  tugas.value = tugas.value.filter((tugas) => tugas.id !== id)
}

</script>

<template>
  <div>

    <input type="text" v-model="newTugas" @keyup.enter="tambahTugas" placeholder="Tambah Tugas">
    <button @click="tambahTugas">Tambah Tugas</button>

    <ul>
      <li v-for="tugas in tugas" :key="tugas.id">
        <input type="checkbox" v-model="tugas.status">
        {{ tugas.nama }} - {{ tugas.status ? 'Sudah Selesai' : 'Belum Selesai' }}
        <button @click="hapusTugas(tugas.id)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
