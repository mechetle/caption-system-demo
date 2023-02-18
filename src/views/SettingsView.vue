<template>
  <div class="container about">
    <h1>Settings</h1>

    <h2>Captions:</h2>
    <div v-for="(item, index) in captions" class="caption-obj" :key="index">
      <div class="caption-obj-header">
        <div>{{ index }}:</div>
        <button @click="captions.splice(index, 1)">🗑️</button>
      </div>

      <textarea v-model="captions[index]" type="text"></textarea>
    </div>
    <button @click="captions.push('')">Add caption</button>

    <h2>Duration</h2>
    <input type="text" v-model="durationOfLoop">


  </div>
</template>

<script setup>
import { useSettingsStore } from '@/stores/settings'
const settingsStore = useSettingsStore()
const {captions, durationOfLoop} = settingsStore


</script>

<style scoped>
.caption-obj {
  display: flex;
  flex-direction: column;
  margin-bottom: 1em;
}

.caption-obj textarea {
  min-height: 10em;
}
.caption-obj-header {
  display: flex;
  justify-content: space-between;
}

@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
}
</style>
