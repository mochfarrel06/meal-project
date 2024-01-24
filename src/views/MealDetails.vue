<template>
  <div class="max-w-[800px] mx-auto p-8">
    <h1 class="text-5xl font-bold mb-5">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" :alt="meal.strMeal" class="max-w-full" />
    <div class="grid grid-cols-1 sm:grid-cols-3 text-lg py-2">
      <div>
        <strong class="font-bold">Category:</strong> {{ meal.strCategory }}
      </div>
      <div><strong class="font-bold">Area:</strong> {{ meal.strArea }}</div>
      <div><strong class="font-bold">Tags:</strong> {{ meal.strTags }}</div>
    </div>

    <div class="my-3">
      {{ meal.strInstructions }}
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2">
      <div>
        <h2 class="text-2xl font-semibold mb-3">Ingredients</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)" v-bind:key="ind">
            <li v-if="meal[`strIngredient${ind + 1}`]">
              {{ ind + 1 }} . {{ meal[`strIngredient${ind + 1}`] }}
            </li></template
          >
        </ul>
      </div>
      <div>
        <h2 class="text-2xl font-semibold mb-3">Ingredients</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)" v-bind:key="ind">
            <li v-if="meal[`strMeasure${ind + 1}`]">
              {{ ind + 1 }} . {{ meal[`strMeasure${ind + 1}`] }}
            </li></template
          >
        </ul>
      </div>

      <div class="mt-10">
        <YouTubeButton :href="meal.strYoutube" />
        <a
          :href="meal.strSource"
          target="_blank"
          class="px-3 py-2 rounded border-2 bg-indigo-600 text-white border-indigo-600 hover:bg-indigo-700 transition-colors"
          >View original source</a
        >
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import YouTubeButton from "../components/YouTubeButton.vue";

const route = useRoute();
const meal = ref({});

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0] || {};
  });
});
</script>
