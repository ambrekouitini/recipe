<script lang="ts" setup>
import type { IRecipe } from '../models/recipes.model'

defineProps({
  recipe: {
    type: Object as PropType<IRecipe>,
    required: true,
  },
})
</script>

<template>
  <li class="flex flex-col gap-y-2 p-4 border-2 border-gray-300 rounded-lg shadow-md bg-gradient-to-r from-gray-200 to-gray-300 hover:to-blue-300">
    <div class="flex justify-between items-center">
      <h3 class="text-lg font-semibold text-gray-800">
        {{ recipe.title }}
      </h3>
      <NuxtLink :to="`/recettes/${recipe.slug}`" class="text-black hover:text-gray-600 transition-colors duration-300">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/>
        </svg>
      </NuxtLink>
    </div>
    <NuxtImg :src="recipe.image.url" alt="" class="h-[400px] w-full object-cover rounded-lg" />
    <div class="flex flex-wrap items-center gap-x-2 gap-y-1">
      <span v-for="tag in recipe.tags" :key="tag.id" class="py-1 px-2 bg-gray-200 text-gray-800 rounded-full text-sm">
        {{ tag.name }}
      </span>
      <span class="py-1 px-2 bg-gray-200 text-gray-800 rounded-full text-sm">
        {{ recipe.serving }} portions 
      </span>
    </div>
  </li>
</template>

