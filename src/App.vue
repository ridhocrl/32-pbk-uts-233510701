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
  <input type="text" v-model="newTugas" @keyup.enter="tambahTugas">
  <button @click="tambahTugas">Tambahkan</button>
  <select v-model="filter">
    <option value="semua">Semua</option>
    <option value="selesai">Selesai</option>
    <option value="belum selesai">Belum Selesai</option>
  </select>

  <ul>
    <li v-for="tugas in filterTugas" :key="tugas.id">
      <input type="checkbox" v-model="tugas.completed">
      {{ tugas.text }}
      <button @click="hapusTugas(tugas.id)">Hapus</button>
    </li>
  </ul>
</template>

<style scoped></style>
