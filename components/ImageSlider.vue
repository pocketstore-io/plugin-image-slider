<template>
  <div class="col-span-6">
    <div class="relative w-full aspect-16/9 mx-auto rounded-xl">
      <!-- Images -->
      <div>
        <img :src="images[current]" class="w-full h-full object-cover"/>
      </div>

      <!-- Arrows -->
      <button
          class="absolute top-1/2 left-4 -translate-y-1/2 bg-black/60 text-white px-3 py-2 rounded-full text-2xl"
          @click="prev"
      >
        <font-awesome-icon icon="chevron-left"></font-awesome-icon>
      </button>

      <button
          class="absolute top-1/2 right-4 -translate-y-1/2 bg-black/60 text-white px-3 py-2 rounded-full text-2xl"
          @click="next"
      >
        <font-awesome-icon icon="chevron-right"></font-awesome-icon>
      </button>

      <!-- Dots -->
      <div class="absolute bottom-4 w-full flex justify-center gap-3">
      <span
          v-for="(img, index) in images"
          :key="index"
          class="w-3 h-3 rounded-full cursor-pointer transition"
          :class="index === current ? 'bg-white' : 'bg-gray-400'"
          @click="goTo(index)"
      />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome"
import {ref} from 'vue'

const images = [
  'https://image.tmdb.org/t/p/original/6U17IFhOo7omnuD2mrFQIaHx82B.jpg',
  'https://image.tmdb.org/t/p/original/ah3m5E28pE4vsFnNvoTTdVxxT3B.jpg',
  'https://image.tmdb.org/t/p/original/ebg8TF2vYaSVNVLv8WO8omebrjw.jpg'
]

const current = ref(0)

const next = () => {
  current.value = (current.value + 1) % images.length
}

const prev = () => {
  current.value = (current.value - 1 + images.length) % images.length
}

const goTo = (index) => {
  current.value = index
}
</script>
