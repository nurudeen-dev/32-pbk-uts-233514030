<script setup>
import { ref, computed } from 'vue'

const tugas = ref([])
const newTugas = ref('')
const filterStatus = ref('semua')

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

const filterTugas = computed(() => {
  if (filterStatus.value === 'semua') {
    return tugas.value
  } else if (filterStatus.value === 'selesai') {
    return tugas.value.filter((tugas) => tugas.status)
  } else {
    return tugas.value.filter((tugas) => !tugas.status)
  }
})

</script>

<template>
  <div>

    <input type="text" v-model="newTugas" @keyup.enter="tambahTugas" placeholder="Tambah Tugas">
    <button @click="tambahTugas">Tambah Tugas</button>
    <div>
      <button @click="filterStatus = 'semua'">Semua</button>
      <button @click="filterStatus = 'selesai'">Selesai</button>
      <button @click="filterStatus = 'belum selesai'">Belum Selesai</button>
    </div>

    <ul>
      <li v-for="tugas in filterTugas" :key="tugas.id">
        <input type="checkbox" v-model="tugas.status">
        {{ tugas.nama }} - {{ tugas.status ? 'Sudah Selesai' : 'Belum Selesai' }}
        <button @click="hapusTugas(tugas.id)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
