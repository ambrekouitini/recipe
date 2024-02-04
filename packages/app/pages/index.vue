<script lang="ts" setup>
import RecipeCard from '~/components/RecipeCard.vue'
import type { ITag } from '~/models/recipes.model'


// Désactivez la vérification du certificat auto-signé
process.env['NODE_TLS_REJECT_UNAUTHORIZED'] = '0';

const { find } = useStrapi4()
const search = useSearchStore()

const { data: tags } = useAsyncData(
  'tags',
  () => find<{ data: ITag[] }>('tags'),
)

function addTag(tag: string) {
  if (!search.queryTags.includes(tag))
    search.queryTags.push(tag)
  else
    search.queryTags = search.queryTags.filter(t => t !== tag)
}
</script>

<template>
  <div class="container mx-auto p-8">
    <header class="mb-8">
      <div class="w-full mb-4" role="search">
        <input v-model="search.query" class="w-full p-4 border-2 border-gray-200 rounded-lg outline-none focus:border-blue-500 transition-all duration-300" type="search" placeholder="Chercher une recette...">
      </div>
      <div class="flex flex-wrap">
        <button
          v-for="tag in tags?.data" :key="tag.id"
          :class="{'bg-blue-500 text-white': search.queryTags.includes(tag.slug), 'bg-gray-200 text-gray-800': !search.queryTags.includes(tag.slug)}"
          @click="addTag(tag.slug)"
          class="text-sm md:text-base py-2 px-4 rounded-full cursor-pointer mr-2 mb-2 hover:bg-gray-300 transition-colors duration-300">
          {{ tag.name }}
        </button>
        <button @click="search.resetTags" class="bg-blue-500 text-white font-bold py-2 px-4 rounded hover:bg-blue-700 transition duration-300 ease-in-out">
          Réinitialiser les tags
        </button>
      </div>
    </header>
    <main>
      <div class="results">
        <ul class="grid grid-cols-1 md:grid-cols-3 gap-4" v-if="search.sortedByTags.length">
          <RecipeCard
            v-for="recipe in search.sortedByTags"
            :key="recipe.id"
            :recipe="recipe"
            class="transition-transform duration-300 hover:scale-105"
          />
        </ul>
        <p v-else>Aucun résultat pour cette recherche</p>
      </div>
    </main>
  </div>
</template>
