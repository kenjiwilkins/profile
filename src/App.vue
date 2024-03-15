<script setup lang="ts">
import { ref } from "vue";
import HomeSection from "./components/HomeSection.vue";

// data
const selected = ref(0);
const navigationItems = ["HOME", "ABOUT", "CONTACT"];

// methods
const selectNavItem = (index: number) => {
  selected.value = index;
};
</script>

<template>
  <div class="container">
    <header>
      <nav class="navigation">
        <ul>
          <li
            v-for="(nav, index) in navigationItems"
            :class="selected === index && 'selected'"
            @click="selectNavItem(index)"
          >
            <span>
              {{ nav }}
            </span>
          </li>
        </ul>
      </nav>
    </header>
    <main>
      <HomeSection />
    </main>
    <footer>f</footer>
  </div>
</template>

<style scoped lang="scss">
.container {
  font-family: sans-serif;
  height: 100vh;
  width: 100vw;
  position: relative;
  background: rgb(255, 255, 255);
  background: linear-gradient(
    270deg,
    rgba(255, 255, 255, 1) 0%,
    rgba(228, 228, 228, 1) 80%,
    rgba(232, 232, 224, 1) 100%
  );
}

.navigation {
  ul {
    padding-left: 8px;
    display: flex;
    flex-direction: column;
    gap: 24px;
    li {
      position: relative;
      font-weight: bold;
      padding-right: 4px;
      width: fit-content;
      border-right: 0px solid white;
      transition: border-right 0.3s ease;
      &.selected {
        border-right: 2px solid white;
        animation: selectBar 1s ease infinite;
      }
      &::after {
        content: "";
        position: absolute;
        top: 50%;
        left: -200%;
        width: 200%;
        height: 0px;
        transform: translateY(-50%);
        background-color: white;
        z-index: -1;
      }
      &:hover {
        cursor: pointer;
        &::after {
          height: 2px;
          left: -100%;
          transition: height 0.2s ease-in-out, left 0.2s ease-in-out;
        }
      }
    }
  }
}

header {
  position: fixed;
  top: 50%;
  transform: translateY(-50%);
  left: 0;
}
main {
}
footer {
  position: fixed;
  bottom: 0;
  left: 0;
}

@keyframes selectBar {
  0% {
    padding-right: 2px;
  }
  80% {
    padding-right: 8px;
  }
}
</style>
