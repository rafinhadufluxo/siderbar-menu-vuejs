<template>
  <div :class="['app', is_expanded ? 'menu-expanded' : 'menu-collapsed']">
    <!-- Sidebar -->
    <AppSidebar @toggle-menu="toggleMenu" />

    <!-- Content -->
    <main>
      <router-view />
    </main>
  </div>
</template>

<script setup>
import { ref } from "vue";
import AppSidebar from "./components/Sidebar.vue";

const is_expanded = ref(localStorage.getItem("is_expanded") === "true");

const toggleMenu = () => {
  is_expanded.value = !is_expanded.value;
  localStorage.setItem("is_expanded", is_expanded.value);
};
</script>

<style lang="scss">
:root {
  --primary: #4ade80;
  --primary-alt: #22c55e;
  --grey: #64748b;
  --dark: #1e293b;
  --dark-alt: #334155;
  --light: #f1f5f9;
  --sidebar-width: 300px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira sans", sans-serif;
}

body {
  background: var(--light);
}

button {
  cursor: pointer;
  appearance: none;
  border: none;
  outline: none;
  background: none;
}

.app {
  display: flex;

  &.menu-expanded {
    main {
      display: none;
    }
  }

  &.menu-collapsed {
    main {
      flex: 1 1 0;
      padding: 2rem;

      @media (max-width: 1024px) {
        padding-left: 6rem;
      }
    }
  }
}
</style>
