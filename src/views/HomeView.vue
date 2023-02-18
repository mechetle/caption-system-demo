
<template>
  <main>
    <div id="stuff">
      <template v-for="(item, index) in captions" :key="index">
        <Transition name="fade-up" mode="out-in">
          <Caption v-if="activeCaptionIndex == index" :msg="item"></Caption>
        </Transition>
      </template>
    </div>

    <div id="cool-overlay">
      <p>Active caption:</p>
      <input type="number" v-model="activeCaptionIndex">
    </div>
  </main>
</template>

<script setup>
  import Caption from '../components/Caption.vue';
  import { ref, onMounted } from 'vue'
  
  import { useSettingsStore } from '@/stores/settings'
  const settingsStore = useSettingsStore()
  const {captions, durationOfLoop} = settingsStore
  
  const activeCaptionIndex = ref(0)
  
  
  onMounted(() => {
    setInterval(() => {
      activeCaptionIndex.value++    
      console.log("wtf man")
  
      if (activeCaptionIndex.value == captions.length) {
        activeCaptionIndex.value = 0
      } 
  
    }, durationOfLoop);
    
    console.log("Changed the caption")
  })
  </script>
  
<style scoped>
main {
  height: 100vh;
  position: relative;
}

#cool-overlay {
  position: fixed;
  top: 3em;
  z-index: 500;
  opacity: 0;
}

#stuff {
  bottom: 0;
  position: fixed;
  height: 100%;
  display: flex;
  align-items: flex-end;
}

#stuff:hover + #cool-overlay {
  opacity: 1;
}


.fade-up-enter-active {
  transition: all 0.8s cubic-bezier(0.84, 0.12, 0, 0.96);
  /* transition-delay: 0.35s; */
}

.fade-up-leave-active {
  transition: all 0.8s cubic-bezier(0.84, 0.12, 0, 0.96);
}

.fade-up-enter-from {
  transform: translateY(200px);
  opacity: 0;
}
.fade-up-leave-to {
  transform: translateY(-20px);
  opacity: 0;
}
</style>
  