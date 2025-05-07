<script setup>
import { ref, computed } from 'vue'

const tugas = ref([])
const newTugas = ref('')
const filterStatus = ref('semua')

const tambahTugas = () => {
  if (newTugas.value.trim()) {
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
  <div class="min-h-screen bg-gray-900 p-6 text-white flex items-center justify-center">
    <div
      class="min-h-[32rem] w-full max-w-6xl grid grid-cols-1 md:grid-cols-2 gap-6 bg-amber-50 rounded-xl p-6 shadow-xl">

      <div class="bg-amber-600 p-6 rounded-lg shadow-lg flex flex-col gap-6 justify-between">
        <div>
          <h2 class="text-xl font-bold mb-2 text-white">Tambah Tugas</h2>
          <input type="text" v-model="newTugas" @keyup.enter="tambahTugas" placeholder="Tulis tugas baru..."
            class="w-full p-2 rounded-md text-gray-900 placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-amber-300" />
          <button @click="tambahTugas"
            class="w-full mt-3 bg-white text-amber-700 font-semibold py-2 rounded-md hover:bg-amber-100 transition">
            ➕ Tambah Tugas
          </button>
        </div>

        <div class="flex flex-col gap-2 mt-6">
          <h3 class="text-white font-semibold mb-1">Filter Tugas</h3>
          <button @click="filterStatus = 'semua'"
            :class="filterStatus === 'semua' ? 'bg-white text-amber-700' : 'bg-amber-500 text-white'"
            class="py-2 rounded-md font-medium hover:bg-amber-400 transition">
            Semua
          </button>
          <button @click="filterStatus = 'selesai'"
            :class="filterStatus === 'selesai' ? 'bg-white text-amber-700' : 'bg-amber-500 text-white'"
            class="py-2 rounded-md font-medium hover:bg-amber-400 transition">
            Selesai
          </button>
          <button @click="filterStatus = 'belum selesai'"
            :class="filterStatus === 'belum selesai' ? 'bg-white text-amber-700' : 'bg-amber-500 text-white'"
            class="py-2 rounded-md font-medium hover:bg-amber-400 transition">
            Belum Selesai
          </button>
        </div>
      </div>

      <div class="bg-amber-950 p-6 rounded-lg shadow-lg h-120 overflow-y-auto ">
        <h2 class="text-xl font-bold text-white mb-4">📋 Daftar Tugas</h2>

        <ul class="space-y-3">
          <li v-for="tugas in filterTugas" :key="tugas.id"
            class="bg-gray-800 px-4 py-3 rounded-md flex items-center justify-between transition duration-200 hover:bg-gray-700">
            <!-- Konten kiri: checkbox + nama -->
            <div class="flex items-center gap-3">
              <input type="checkbox" v-model="tugas.status" class="accent-amber-500 w-5 h-5" />
              <span class="text-white" :class="{ 'line-through text-gray-400 italic': tugas.status }">
                {{ tugas.nama }}
              </span>
            </div>

            <button @click="hapusTugas(tugas.id)" class="text-red-400 hover:text-red-600 font-bold text-lg"
              title="Hapus tugas">
              ✕
            </button>
          </li>
        </ul>
      </div>


    </div>
  </div>
</template>
