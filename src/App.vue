<script setup>
import CountdownHeader from "@/components/CountdownHeader.vue";
import CountdownSegment from "@/components/CountdownSegment.vue";
import { ref } from "vue";

const today = ref(new Date())
const newYearDate = ref(new Date(`${today.value.getFullYear() + 1}-01-01`))
const days = ref(Math.floor((newYearDate.value - today.value) / (1000 * 60 * 60 * 24)))
const hours = ref(23 - today.value.getHours())
const minutes = ref(59 - today.value.getMinutes())
const seconds = ref(59 - today.value.getSeconds())

setInterval(() => {
  seconds.value --
  if(seconds.value < 0){
    minutes.value --
    seconds.value = 59
  }
  if(minutes.value < 0){
    hours.value --
    minutes.value = 59
  }
  if(hours.value < 0){
    days.value --
    hours.value = 59
  }
}, 1000);
</script>
<template>
  <div class="app-wrapper">
    <div class="countdown-box">
      <CountdownHeader />
      <main class="flex justify-center">
        <CountdownSegment data-test="days" label="days" :numb="days" />
        <CountdownSegment data-test="hours" label="hours" :numb="hours" />
        <CountdownSegment data-test="minutes" label="minutes" :numb="minutes" />
        <CountdownSegment data-test="seconds" label="seconds" :numb="seconds" />
      </main>
    </div>
  </div>
</template>

<style scoped>
.app-wrapper {
  @apply flex items-center justify-center w-full h-full p-10;
}
.countdown-box {
  @apply shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px];
}
body {
  @apply bg-gray-100;
}
</style>
