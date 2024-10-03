<script setup>
import { RouterLink, useRoute } from 'vue-router'
import VueLogo from '@/assets/logo.svg'

const isActiveLink = (routePath) => {
  const route = useRoute()
  return route.path === routePath
}
</script>

<template>
  <nav>
    <div class="navbar flex gap-20 items-center justify-between py-3 px-3 bg-orange-800">
      <header>
        <RouterLink to="/">
          <img :src="VueLogo" alt="Company Logo" class="w-12 md:w-20" />
        </RouterLink>
      </header>
      <div class="nav-links flex items-center justify-between">
        <div class="links text-white flex gap-3 mr-3">
          <RouterLink
            to="/"
            :class="[
              isActiveLink('/') ? 'bg-slate-900' : 'hover:text-white hover:bg-slate-800',
              'p-2',
              'rounded-lg',
              'duration-300'
            ]"
            >Home</RouterLink
          >
          <RouterLink
            to="/weather"
            :class="[
              isActiveLink('/weather') ? 'bg-slate-900' : 'hover:text-white hover:bg-slate-800',
              'p-2',
              'rounded-lg',
              'duration-300'
            ]"
            >Weather</RouterLink
          >
          <RouterLink
            to="/task"
            :class="[
              isActiveLink('/task') ? 'bg-slate-900' : 'hover:text-white hover:bg-slate-800',
              'p-2',
              'rounded-lg',
              'duration-300'
            ]"
            >Tasks</RouterLink
          >
          <RouterLink
            to="/movie"
            :class="[
              isActiveLink('/movie') ? 'bg-slate-900' : 'hover:text-white hover:bg-slate-800',
              'p-2',
              'rounded-lg',
              'duration-300'
            ]"
            >Movies</RouterLink
          >
        </div>
      </div>
    </div>
  </nav>
</template>

<style lang="scss" scoped>
nav {
  .isActive {
    background-color: rgb(15, 23, 42);
  }
}
</style>
