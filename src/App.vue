<script setup>
import { items } from "./movies.json";
import { computed, ref } from "vue";

/*
 This is an Icon that you can use to represent the stars if you like
 otherwise you could just use a simple ⭐️ emoji, or * character.
*/
// import { StarIcon } from "@heroicons/vue/24/solid";
import StarIcon from './StarIcon.vue';


const setRating = (clicked) => {
  currentRating = clicked ? currentRating + 1 : currentRating - 1;
};

let currentRating = ref(0);


//  Computed

const applyClassToAllStars = computed(() => {
  return currentRating.value === 5;
});

const getStarCount = (movie) => {
  return Math.round(movie.rating);
};


const handleImageError = (event) => {
  event.target.src = "https://cdnb.artstation.com/p/marketplace/presentation_assets/000/835/277/large/file.jpg?1618411955";
};
</script> 

<template>
  <br>
  <div class="flex items-center justify-center">
    <h1 class="text-3xl text-center">Chris Vue Movies App</h1>
  </div>
  <br> <br>

  <div class="flex items-center justify-center">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">

      <div class="max-w-sm rounded overflow-hidden shadow-lg border-dashed border-blue-500"
           v-for="item in items">
        <img class="w-full h-48 object-cover"
             :src="item.image"
             alt="Image"
             @error="handleImageError">
        <div class="px-6 py-4">


          <span v-for="genre in item.genres"
                class="inline-block px-2 py-1 text-white text-xs bg-purple-600 rounded-full mr-2 mb-2"
                :key="genre">
            {{ genre }}
          </span>


          <h3 class="font-bold text-xl mb-2">{{ item.name }}</h3>
          <p class="text-gray-700 text-base">{{ item.description }}.</p>
        </div>


        <div class="flex items-center justify-between">


         <span class="m-6">Rating: <br>[{{ getStarCount(item) }} / 5]</span>
          <div class="flex space-x-1 m-6">


        <StarIcon
          v-for="index in 5"
          :key="index"
          :clicked="index <= currentRating"
          :index="index"
          @toggle="setRating"
          class="star-button"
          :class="{ 'class-for-all-stars': applyClassToAllStars }"
        />


      </div> 
        </div>
      </div>

    </div>

  </div>
</template>
