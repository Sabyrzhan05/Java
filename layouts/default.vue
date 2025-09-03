<template>
  <header class="z-[1100] flex flex-row text-white font-bold w-full items-center relative bg-gradient-to-r from-blue-900 via-blue-700 to-cyan-600
    max-sm:justify-beetween max-sm:relative p-4 shadow-2xl">


    <div class="basis-1/4 items-center justify-start px-8 min-w-48 max-sm:basis-auto flex items-center gap-4">
      <img src="assets/image/hydro.png"
        class="w-12 h-12 bg-transparent drop-shadow-lg transform hover:scale-110 transition-transform">
      <span
        class="text-2xl font-light tracking-wider bg-gradient-to-r from-cyan-300 to-white bg-clip-text text-transparent playfair-font">
        Hydrology of Kozybayev
      </span>
    </div>

    <div class="basis-1/4 max-sm:basis-auto"></div>


    <nav :class="{
      'z-[1200] basis-1/2 flex flex-row items-center justify-end px-8 gap-8': true,
      'max-sm:hidden': !burger,
      'max-sm:absolute max-sm:top-full max-sm:left-0 max-sm:w-full max-sm:flex-col max-sm:gap-0 max-sm:bg-blue-800 max-sm:px-0 max-sm:shadow-2xl max-sm:py-4': burger
    }">
      <NuxtLink to="/"
        class="my-auto p-3 rounded-xl transition-all duration-300 hover:bg-cyan-500 hover:shadow-2xl hover:scale-105 
        bg-blue-600/20 backdrop-blur-sm border border-cyan-400/30 max-sm:w-full max-sm:text-center max-sm:mx-4 max-sm:mb-2"
        @click="closeMobileMenu">
        Coordinates
      </NuxtLink>

      <div class="relative">
        <div
          class="my-auto p-3 rounded-xl transition-all duration-300 hover:bg-cyan-500 hover:shadow-2xl hover:scale-105 
          bg-blue-600/20 backdrop-blur-sm border border-cyan-400/30 cursor-pointer max-sm:w-full max-sm:text-center max-sm:mx-4 max-sm:mb-2"
          @click="toggleSubmenu">
          Hydrology
        </div>
        <div
          class="flex flex-col absolute left-0 top-full bg-gradient-to-b from-blue-800 to-cyan-700 text-white w-64 text-center rounded-2xl 
          shadow-2xl border-2 border-cyan-400/50 mt-1 backdrop-blur-md overflow-hidden max-sm:relative max-sm:w-11/12 max-sm:mx-auto max-sm:mt-2 max-sm:left-auto"
          v-show="submenu">
          <NuxtLink to="/lab3" class="my-auto p-4 border-b border-cyan-400/30 hover:bg-cyan-500/50 hover:scale-105 transition-all 
            max-sm:w-full max-sm:border-t max-sm:border-cyan-400/30" @click="closeAllMenus">Water Level</NuxtLink>
          <NuxtLink to="/lab4" class="my-auto p-4 border-b border-cyan-400/30 hover:bg-cyan-500/50 hover:scale-105 transition-all 
            max-sm:w-full max-sm:border-t max-sm:border-cyan-400/30" @click="closeAllMenus">Transparency</NuxtLink>
          <NuxtLink to="/lab5" class="my-auto p-4 border-b border-cyan-400/30 hover:bg-cyan-500/50 hover:scale-105 transition-all 
            max-sm:w-full max-sm:border-t max-sm:border-cyan-400/30" @click="closeAllMenus">Temperature</NuxtLink>
          <NuxtLink to="/lab6" class="my-auto p-4 hover:bg-cyan-500/50 hover:scale-105 transition-all 
            max-sm:w-full max-sm:border-t max-sm:border-cyan-400/30" @click="closeAllMenus">Conductivity</NuxtLink>
        </div>
      </div>

      <NuxtLink to="/inform"
        class="my-auto p-3 rounded-xl transition-all duration-300 hover:bg-cyan-500 hover:shadow-2xl hover:scale-105 
        bg-blue-600/20 backdrop-blur-sm border border-cyan-400/30 max-sm:w-full max-sm:text-center max-sm:mx-4 max-sm:mb-2"
        @click="closeMobileMenu">
        Patogens
      </NuxtLink>
    </nav>


    <div @click="toggleBurger"
      class="hidden max-sm:flex max-sm:flex-col max-sm:mr-6 max-sm:justify-center max-sm:items-center max-sm:w-10 max-sm:h-8 cursor-pointer group">
      <span :class="['h-1 w-full bg-cyan-300 rounded-full transition-all duration-300',
        burger ? 'rotate-45 translate-y-2' : '']"></span>
      <span :class="['h-1 w-full bg-cyan-300 rounded-full transition-all duration-300 mt-2',
        burger ? 'opacity-0' : '']"></span>
      <span :class="['h-1 w-full bg-cyan-300 rounded-full transition-all duration-300 mt-2',
        burger ? '-rotate-45 -translate-y-2' : '']"></span>
    </div>
  </header>

  <main
    class="z-[2] flex p-2 h-screen bg-gradient-to-br from-blue-900/10 via-cyan-700/10 to-blue-800/10 backdrop-blur-sm">
    <slot />
  </main>

  <footer class="flex flex-row w-full bg-gradient-to-r from-blue-900 via-blue-700 to-cyan-600 
    items-center justify-center px-12 py-6 shadow-2xl">


    <div class="flex gap-8">
      <a href="https://www.youtube.com/" class="transition-all hover:scale-125 hover:drop-shadow-cyan">
        <img src="assets/image/youtube.png" class="w-10 h-10 drop-shadow-lg" />
      </a>
      <a href="https://github.com/" class="transition-all hover:scale-125 hover:drop-shadow-cyan">
        <img src="assets/image/hub.png" class="w-10 h-10 drop-shadow-lg" />
      </a>
      <a href="https://www.facebook.com/" class="transition-all hover:scale-125 hover:drop-shadow-cyan">
        <img src="assets/image/fc.png" class="w-10 h-10 drop-shadow-lg bg-transparent" />
      </a>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { useHead } from '#app';
import { ref } from 'vue';

const burger = ref<boolean>(false);
const submenu = ref<boolean>(false);

const toggleBurger = () => {
  burger.value = !burger.value;
  if (burger.value) {
    submenu.value = false;
  }
}

const toggleSubmenu = () => {
  submenu.value = !submenu.value;
}

const closeAllMenus = () => {
  burger.value = false;
  submenu.value = false;
}

const closeMobileMenu = () => {
  burger.value = false;
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@300;400;600&display=swap');

.playfair-font {
  font-family: 'Playfair Display', serif;
}

.hover\:drop-shadow-cyan:hover {
  filter: drop-shadow(0 0 8px rgba(34, 211, 238, 0.8));
}

@media (min-width: 641px) {
  .max-sm\:flex {
    display: none !important;
  }
}

@media (min-width: 641px) {
  .relative:hover .absolute {
    display: flex !important;
  }

  .relative .absolute {
    display: none;
  }
}

@media (max-width: 640px) {
  .max-sm\:hidden {
    display: none;
  }
}
</style>