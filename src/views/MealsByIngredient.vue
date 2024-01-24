<template>
  <!-- <div class="p-8">
    <h1 class="text-4xl font-semibold mb-4">Meals by ingredient</h1>
    <router-link
      :to="{
        name: 'byIngredient',
        params: { ingredient: ingredient.idIngredient },
      }"
      v-for="ingredient of ingredients"
      :key="ingredient.idIngredient"
      class="block bg-white rounded p-3 mb-3 shadow-sm"
    >
      <h3 class="text-2xl font-semibold mb-2">
        {{ ingredient.strIngredient }}
      </h3>
      <p>{{ ingredient.strDescription }}</p>
    </router-link>
  </div> -->
  <!-- <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
  <div v-if="!meals.length" class="flex justify-center text-gray-400">
    There are no meals
  </div> -->
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted } from "vue";
import { useRoute } from "vue-router";
import store from "../store";
import Meals from "../components/Meals.vue";

const route = useRoute();
const meals = computed(() => store.state.mealsByIngredient);

onMounted(() => {
  store.dispatch("getMealsByIngredient", route.params.ingredient);
});
</script>
