<script setup lang="ts">
import Timer from '@/components/Timer.vue';
import { ref, onMounted, onUnmounted } from "vue";

const gradDay = "29 Nov 2024";
const RemainingDays = ref("");
const RemainingHours = ref("");
const RemainingMinutes = ref("");
const RemainingSeconds = ref("");

function countDown() {
  const gradDayDate: Date = new Date(gradDay);
  const currentDate: Date = new Date();

  const totalSeconds = (gradDayDate.getTime() - currentDate.getTime())/1000;

  const days = Math.floor(totalSeconds / 3600 / 24);
  const hours = Math.floor(totalSeconds / 3600) % 24;
  const minutes = Math.floor(totalSeconds / 60) % 60;
  const seconds = Math.floor(totalSeconds) % 60;

  RemainingDays.value = setTime(days);
  RemainingHours.value = setTime(hours);
  RemainingMinutes.value = setTime(minutes);
  RemainingSeconds.value = setTime(seconds);

  console.log(days,hours,minutes,seconds)
}

function setTime(value: number) {
  return value >= 10 ? value.toString() : `0${value}`
}

let timeInterval : ReturnType<typeof setInterval>;
onMounted(()=> {
  timeInterval = setInterval(countDown,1000)
})

onUnmounted(()=> {
  clearInterval(timeInterval)
})
</script>

<template>
  <div class="container">

    <div class="title">
      Graduation Count Down
    </div>

    <div class="timer">
      <Timer :count="RemainingDays" label="Days"/>
      <Timer :count="RemainingHours" label="Hours"/>
      <Timer :count="RemainingMinutes" label="Minutes"/>
      <Timer :count="RemainingSeconds" label="Seconds"/>
    </div>
  </div>
  
</template>


<style>
@import url('https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap');



body{
  margin: 0;
  font-family: 'Lato', sans-serif;
}

.container {
  height: 100vh;
  background-image: url("@/assets/bg-timer.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.title{
  font-size: 5rem;
  font-weight: bold;
  color: rgb(221, 15, 94);
  text-align: center;
  
}

.timer {
  display: flex;
  align-items: center;
  justify-content: space-around;
}
</style>
