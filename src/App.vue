<script setup>
import SplashScreen from '@/components/SplashScreen.vue'
import { defineAsyncComponent } from 'vue'
const Home = defineAsyncComponent(() => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(import('./components/Home.vue'))
    }, 2500)
  })
})
</script>

<template>
  <main>
    <Suspense>
      <template #default><Home /></template>
      <template #fallback><SplashScreen /></template>
    </Suspense>
  </main>
</template>

<style>
html,
body,
.app {
  width: 100%;
  min-height: 100vh;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}

* {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
}
</style>
