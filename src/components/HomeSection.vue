<script setup lang="ts">
import { ref, onMounted } from "vue";

// data
const loadingProgress = ref(0);
const name = ref(["Michael", "Kenji", "Wilkins"]);

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
        <div class="home-section-container">
          <div class="names">
            <h1>
              <span v-for="n in name" :key="n">{{ n }}</span>
            </h1>
            <h2>
              <span>Frontend Developer</span>
            </h2>
          </div>
        </div>
        <div class="home-section-container">
          <h1>About Section</h1>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla
            tincidunt, nunc nec aliquam lacinia, nunc nunc lacinia.
          </p>
        </div>
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
  background-color: #3b3b3b;
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
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 24px;
  .home-section-container {
    width: 50%;
    display: inline-block;
    padding: 16px;

    .names {
      position: relative;
      height: 100%;
      font-size: 48px;
      h1 {
        display: flex;
        gap: 8px;
      }
    }
  }
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
