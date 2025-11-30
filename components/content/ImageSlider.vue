<template>
  <div class="col-span-6">
    <div class="relative w-full aspect-16/9 mx-auto rounded-xl">
      <!-- Images -->
      <div>
        <img :src="getMediaUrl(props.images[current],'media')" class="w-full h-full object-cover"/>
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
          v-for="(_, index) in props.images"
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
import {getMediaUrl} from '~/utils/pocketbase'

const props = defineProps({
  images: {type: Array, required: true},
});

const current = ref(0)

const next = () => {
  current.value = (current.value + 1) % props.images.length
}

const prev = () => {
  current.value = (current.value - 1 + props.images.length) % props.images.length
}

const goTo = (index) => {
  current.value = index
}
</script>
