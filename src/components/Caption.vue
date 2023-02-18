<template>
    <div class="hehehe">
      <h1>{{ msg }}</h1>        
    </div>
</template>

<script setup>
defineProps({
  msg: {
    type: String,
    //required: true
  }
})
</script>

<style scoped>
.hehehe {
  position: absolute;
  width: 100vw;
}
</style>