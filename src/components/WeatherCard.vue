<script setup>
import { ref } from 'vue'
import BorderLine from './BorderLine.vue'
import WeatherForcastDay from './WeatherForcastDay.vue'
import WeatherInfo from './WeatherInfo.vue'

defineProps({
  place: Object
})

const emit = defineEmits(['delete-place'])

const showDetail = ref(false)

const removePlace = (placeName) => {
  emit('delete-place', placeName)
  showDetail.value = false
}
</script>

<template>
  <div :class="place.current.is_day === 1 ? 'bg-day' : 'bg-night'" class="text-white p-4 md:p-6 lg:p-8 rounded-lg shadow-lg gap-4 md:gap-6 mb-6 relative overflow-hidden sm:w-72">
    <!-- Location & time -->
    <div class="mb-2 flex flex-col md:flex-row  justify-between items-center">
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-location-dot"></i>
        <h1 class="text-lg md:text-xl lg:text-2xl">{{ place.location.name }}</h1>
      </div>
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-clock"></i>
        <h1 class="text-lg md:text-xl lg:text-2xl">
          {{ new Date(place.location.localtime).getHours() }}:
          {{ new Date(place.location.localtime).getMinutes() }}
        </h1>
      </div>
    </div>

    <!-- current weather -->
    <div class="text-center">
      <img :src="place.current.condition.icon" alt="icon" class="w-16 md:w-20 lg:w-24 mx-auto -mb-4 md:-mb-6 lg:-mb-8" />
      <h1 class="text-4xl md:text-5xl lg:text-7xl mb-2">{{ Math.round(place.current.temp_c) }}&deg;</h1>
      <p class="text-base md:text-lg lg:text-xl">{{ place.current.condition.text }}</p>
    </div>

    <BorderLine />

    <!-- forecast -->
    <div v-for="(day, idx) in place.forecast.forecastday" :key="idx">
      <WeatherForcastDay :day="day" />
    </div>

    <!-- info -->
    <Transition name="fade">
      <div v-show="showDetail">
        <WeatherInfo
          :place="place"
          @close-info="showDetail = false"
          @remove-place="removePlace(place.location.name)"
        />
      </div>
    </Transition>

    <!-- forecast btn -->
    <div class="flex justify-center md:justify-end items-center gap-1 mt-4 md:mt-6 lg:mt-8">
      <button @click="showDetail = true">
        More <i class="fa-solid fa-arrow-right text-xs md:text-sm -mb-px"></i>
      </button>
    </div>
  </div>
</template>

<style scoped>

.bg-day{
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg, #8ec5fc 0%,#e0c3fc 100% );
}
.bg-night{
  background-color: #07223d;
  background-image: linear-gradient(62deg, #0a2a4a 0%,#270845 100% );
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}


/* You can add further media queries for different screen sizes */
</style>



