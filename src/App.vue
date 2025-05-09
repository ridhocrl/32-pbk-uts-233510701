<script setup>
import { ref } from 'vue'

const tugas = ref([])
const newTugas = ref('')

const tambahTugas = () =>{
  if (newTugas.value.trim() !== '') {
    tugas.value.push({
      id: Date.now(),
      text: newTugas.value,
      completed: false
    })
    newTugas.value = ''
  }
}
</script>

<template>
  <input type="text" v-model="newTugas" @keyup.enter="tambahTugas">
  <button @click="tambahTugas">Tambahkan</button>

  <ul>
    <li v-for="tugas in tugas" :key="tugas.id">
      {{  tugas.text }}
    </li>
  </ul>
</template>

<style scoped>

</style>
