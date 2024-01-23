<template>
  <div class="p-8 pb-0">
    <input
      type="text"
      v-model="keyword"
      class="rounded border-2 border-gray-200 w-full"
      placeholder="Search for meals"
      @change="searchMeals"
    />
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <div
      v-for="meal of meals"
      :key="meal.idMeal"
      class="bg-white shadow rounded-xl overflow-hidden"
    >
      <router-link to="/">
        <img
          :src="meal.strMealThumb"
          :alt="meal.strMeal"
          class="w-full h-48 object-cover"
        />
      </router-link>
      <div class="p-3">
        <h3 class="font-semibold">{{ meal.strMeal }}</h3>
        <p class="mb-4">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptatibus,
          quaerat!
        </p>
        <div class="mb-4">
          <a
            :href="meal.strYoutube"
            target="_blank"
            class="px-3 py-2 rounded border-2 bg-red-600 text-white border-red-600 hover:bg-red-700 transition-colors"
            >Youtube</a
          >
          <router-link
            to="/"
            class="px-3 py-2 rounded border-2 bg-purple-600 text-white border-purple-600 hover:bg-purple-700 transition-colors"
          >
            View
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import { useRoute } from "vue-router";

const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  store.dispatch("searchMeals", keyword.value);
}

onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>
