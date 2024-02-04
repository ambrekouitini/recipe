<script lang="ts" setup>
// const links = [
//   {
//     id: 1,
//     title: 'Documentation',
//     url: '/start',
//   },
//   {
//     id: 2,
//     title: 'Exemple de recherche',
//     url: '/exemple-recherche',
//   },
// ]
</script>

<template>
  <nav class="w-full bg-white py-9 shadow-xl">
    <div class="container mx-auto flex items-center justify-between">
      <NuxtLink to="/" class="flex items-center text-white">
        <NuxtImg alt="Logo" class="h-12 mr-3" src="/logo.png" />
        <h1 class="text-black text-l md:text-xl font-light">of amber</h1>
      </NuxtLink>
    </div>
  </nav>
</template>


