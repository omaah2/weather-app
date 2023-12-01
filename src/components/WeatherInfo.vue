<script setup>
  defineProps({
    place: Object
  })
</script>

<template>
  <div class=" absolute bg-white/80 backdrop-blur-sm text-slate-900 inset-x-0 bottom-0 rounded-t-lg p-8">
    <!-- Close button -->
    <div class="flex justify-end mb-6 lg:mb-10 sm:mb-4">
      <button @click="$emit('close-info')" class="p-1">
        <i class="fa-solid fa-xmark text-xl"></i>
      </button>
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 lg:gap-10 sm:gap-4">
      <!-- Wind speed -->
      <div class="text-center">
        <i class="fa-solid fa-wind mb text-2xl"></i>
        <p class="text-xl font-bold">{{ place.current.wind_kph }} km/h</p>
        <p>wind</p>
      </div>
      <!-- Humidity level -->
      <div class="text-center">
        <i class="fa-solid fa-droplet mb text-2xl"></i>
        <p class="text-xl font-bold">{{ place.current.humidity }}%</p>
        <p>humidity</p>
      </div>
      <!-- Precipitation -->
      <div class="text-center">
        <i class="fa-solid fa-umbrella mb text-2xl"></i>
        <p class="text-xl font-bold">{{ place.current.precip_mm }}mm</p>
        <p>precipitation</p>
      </div>
      <!-- Wind direction -->
      <div class="text-center">
        <i class="fa-solid fa-fan mb text-2xl"></i>
        <p class="text-xl font-bold">{{ place.current.wind_dir }}</p>
        <p>direction</p>
      </div>
      <!-- Feels like -->
      <div class="text-center">
        <i class="fa-solid fa-temperature-half mb text-2xl"></i>
        <p class="text-xl font-bold">{{ Math.round(place.current.feelslike_c) }}</p>
        <p>Feels</p>
      </div>
      <!-- UV -->
      <div class="text-center">
        <i class="fa-solid fa-sun mb text-2xl"></i>
        <p class="text-xl font-bold">{{ place.current.uv }}</p>
        <p>UV index</p>
      </div>
    </div>
    <!-- Last update and delete -->
    <div class="flex justify-between items-center mt-6 lg:mt-10">
      <h3 class="text-slate-900/50 text-sm lg:text-base">Last update: {{ place.current.last_updated }}</h3>
      <button @click="$emit('remove-place')">
        <i class="fa-solid fa-trash"></i>
      </button>
    </div>
  </div>
</template>

<style scoped>
/* You can add any additional scoped styles here */
@media screen and (max-width: 639px) {
  .absolute {
    scale: 0.9;
    top: 10px;
    padding: 0;
    
  }
  .text-center{
    font-size: 14px;
  }
  .text-xl{
    font-size: 16px;
  }
  .grid{

  }
}
</style>





