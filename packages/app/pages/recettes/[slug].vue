<script lang="ts" setup>
import type { RecipeData } from '~/models/recipes.model'
const { findOne } = useStrapi4()
const route = useRoute()

// Désactivez la vérification du certificat auto-signé
process.env['NODE_TLS_REJECT_UNAUTHORIZED'] = '0';

const { data: recipe, pending } = useAsyncData(
  'recipe',
  () => findOne<RecipeData>(`recipes/${route.params.slug}`),
)

const formatText = (text) => {
  return text.replace(/\n/g, '<br>');
}
</script>

<template>
  <div class="container mx-auto p-8">
    <template v-if="pending">
      <p class="text-9xl text-center text-gray-500">
        MIAAAM
      </p>
    </template>
    <template v-else>
      <NuxtImg
        :src="recipe.data.image.url" alt="" aria-hidden="true"
        class="h-[500px] object-cover object-center w-full rounded-lg shadow-lg"
      />
      <h1 class="text-3xl font-bold text-gray-800 mt-6 mb-4">
        {{ recipe.data.title }}
      </h1>
      <div class="flex flex-wrap items-center gap-x-2 gap-y-2 mb-4">
        <span v-for="tag in recipe.data.tags" :key="tag.id" class="py-1 px-2 bg-gray-200 rounded-full text-sm text-gray-800">
          {{ tag.name }}
        </span>
      </div>
      <span class="block text-lg text-gray-600 mb-2"> Portions : {{ recipe?.data.serving }}</span>
      <div class="mb-4">
        <h2 class="text-2xl font-semibold text-gray-800 mb-2">Ingrédients</h2>
        <p class="text-gray-700" v-html="formatText(recipe.data.description)"></p>
      </div>
      <div>
        <h2 class="text-2xl font-semibold text-gray-800 mb-2">Description</h2>
        <p class="text-gray-700" v-html="formatText(recipe.data.description)"></p>
      </div>
    </template>
  </div>
</template>
