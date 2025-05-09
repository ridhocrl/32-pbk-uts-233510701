<script setup>
import { ref, computed } from 'vue'

const tugas = ref([])
const newTugas = ref('')
const filter = ref('semua')

const tambahTugas = () => {
  if (newTugas.value.trim() !== '') {
    tugas.value.push({
      id: Date.now(),
      text: newTugas.value,
      completed: false
    })
    newTugas.value = ''
  }
}

const hapusTugas = (id) => {
  tugas.value = tugas.value.filter(tugas => tugas.id !== id)
}

const filterTugas = computed(() => {
  if (filter.value === 'selesai') {
    return tugas.value.filter(tugas => tugas.completed)
  } else if (filter.value === 'belum selesai') {
    return tugas.value.filter(tugas => !tugas.completed)
  } else {
    return tugas.value
  }
})

</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-sky-100 to-purple-100 flex flex-col items-center justify-start py-12 px-4 gap-6 text-gray-800">
    <!-- Input Section -->
    <div class="flex gap-3 items-center w-full max-w-md">
      <input
        type="text"
        v-model="newTugas"
        @keyup.enter="tambahTugas"
        placeholder="Tulis tugas baru..."
        class="flex-1 px-4 py-2 rounded border border-gray-300 focus:outline-none focus:ring-2 focus:ring-purple-400 shadow-sm bg-white"
      />
      <button
        @click="tambahTugas"
        class="bg-purple-500 hover:bg-purple-600 text-white px-4 py-2 rounded shadow transition"
      >
        Tambahkan
      </button>
    </div>

    <!-- Filter -->
    <div class="w-full max-w-md">
      <select
        v-model="filter"
        class="w-full px-4 py-2 rounded border border-gray-300 focus:outline-none focus:ring-2 focus:ring-purple-400 shadow-sm bg-white"
      >
        <option value="semua">📋 Semua</option>
        <option value="selesai">✅ Selesai</option>
        <option value="belum selesai">🕒 Belum Selesai</option>
      </select>
    </div>

    <!-- Tugas List -->
    <ul class="w-full max-w-md space-y-4 mt-4">
      <li
        v-for="tugas in filterTugas"
        :key="tugas.id"
        class="flex justify-between items-center bg-white px-4 py-3 rounded shadow-md hover:shadow-lg transition"
      >
        <div class="flex items-center gap-3">
          <input
            type="checkbox"
            v-model="tugas.completed"
            class="accent-purple-500 w-5 h-5"
          />
          <span
            :class="tugas.completed ? 'line-through text-gray-400' : 'text-gray-800'"
            class="text-base"
          >
            {{ tugas.text }}
          </span>
        </div>
        <button
          @click="hapusTugas(tugas.id)"
          class="text-red-500 hover:text-red-700 transition font-semibold"
        >
          ✖
        </button>
      </li>
    </ul>
  </div>
</template>


<style scoped></style>
