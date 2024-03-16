<script setup lang="ts">
import { ref } from "vue";
import HomeSection from "./components/HomeSection.vue";
import GitHubIcon from "./assets/github.svg";
import LinkedInIcon from "./assets/linkedin.svg";

// data
const selected = ref(0);
const navigationItems = ["ABOUT", "EXPERIENCE", "PROJECTS"];

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
    <footer>
      <div class="icons">
        <a
          href="https://github.com/kenjiwilkins"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img :src="GitHubIcon" alt="GitHub" />
          <span class="sr-only">GitHub</span>
        </a>
        <a
          href="https://www.linkedin.com/in/michael-kenji-wilkins-2a7a8a155/"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img :src="LinkedInIcon" alt="LinkedIn" />
          <span class="sr-only">LinkedIn</span>
        </a>
      </div>
    </footer>
  </div>
</template>

<style scoped lang="scss">
.container {
  color: #3b3b3b;
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
  top: 20%;
  transform: translateY(-50%);
  left: 0;
}
main {
  width: 100%;
  height: 100%;
}
footer {
  position: fixed;
  bottom: 0;
  left: 0;
  padding: 48px 24px;
  .icons {
    display: flex;
    gap: 16px;
    align-items: center;
    a {
      display: flex;
      align-items: center;
      gap: 8px;
      img {
        width: 24px;
        height: 24px;
      }
    }
  }
}

@keyframes selectBar {
  0% {
    padding-right: 2px;
  }
  80% {
    padding-right: 8px;
  }
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
