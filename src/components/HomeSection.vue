<script setup lang="ts">
import { ref, onMounted } from "vue";

// data
const loadingProgress = ref(0);

// lifecycle
onMounted(() => {
  const interval = setInterval(() => {
    loadingProgress.value += 1;
    if (loadingProgress.value === 100) {
      clearInterval(interval);
    }
  }, 50);
});
</script>

<template>
  <div class="background">
    <Transition>
      <div class="loading" v-if="loadingProgress < 100">
        <div class="progress" :style="{ width: `${loadingProgress}%` }"></div>
      </div>
    </Transition>
    <Transition>
      <div v-if="loadingProgress >= 100" class="home-body">
        <h1>Home Section</h1>
        <h2>Some content</h2>
      </div>
    </Transition>
  </div>
</template>

<style scoped lang="scss">
.background {
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transition: opacity 0.5s ease-in-out;
}
.loading {
  width: 15vw;
  height: 1px;
  background-color: grey;
  position: relative;
  .progress {
    position: absolute;
    bottom: 0;
    left: 0;
    height: 100%;
    background-color: white;
  }
}

.home-body {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: red;
}

.v-leave-active,
.v-enter-active {
  transition: opacity 0.5s ease-in-out;
}
.v-leave-to,
.v-enter-from {
  opacity: 0;
}
</style>
