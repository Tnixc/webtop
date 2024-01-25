<script setup lang="ts">
import { ref } from "vue";
let filterPercentage = ref(100);

function clock() {
  const date = new Date();
  const hours = date.getHours();
  const minutes = date.getMinutes();
  const seconds = date.getSeconds();
  const time = `${hours}:${minutes}:${seconds}`;
  const target = document.getElementById("clock");
  if (target) {
    target.innerHTML = time;
  }
}
function date() {
  const date = new Date();
  const day = date.getDate();
  const month = date.getMonth();
  const year = date.getFullYear();
  const dateStr = `${day}/${month+1}/${year}`;
  const target = document.getElementById("date");
  if (target) {
    target.innerHTML = dateStr;
  }
}
setInterval(clock, 1000);
setInterval(date, 1000);

function apply(){
  const value = filterPercentage.value;
  console.log(value);
  document.body.style.filter = `brightness(${value}%)`;
}
</script>
<template>
  <div class="fixed justify-between top-3 left-4 right-4 h-10 bg-zinc-800 rounded-lg ring flex items-center px-3 ring-zinc-900 z-[999] shadow-2xl">
    <div class="flex gap-3">
      <span id="clock"></span>
      <span id="date"></span>
    </div>
    <div class="flex gap-3 fixed top-5 left-1/2 -translate-x-1/2">
      <h1>Tnixc's Website</h1>
    </div>
    <div class="flex gap-3">
      <p>Filter percentage: {{ filterPercentage }}%</p>
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="#ffffff" viewBox="0 0 256 256"><path d="M120,40V16a8,8,0,0,1,16,0V40a8,8,0,0,1-16,0Zm72,88a64,64,0,1,1-64-64A64.07,64.07,0,0,1,192,128Zm-16,0a48,48,0,1,0-48,48A48.05,48.05,0,0,0,176,128ZM58.34,69.66A8,8,0,0,0,69.66,58.34l-16-16A8,8,0,0,0,42.34,53.66Zm0,116.68-16,16a8,8,0,0,0,11.32,11.32l16-16a8,8,0,0,0-11.32-11.32ZM192,72a8,8,0,0,0,5.66-2.34l16-16a8,8,0,0,0-11.32-11.32l-16,16A8,8,0,0,0,192,72Zm5.66,114.34a8,8,0,0,0-11.32,11.32l16,16a8,8,0,0,0,11.32-11.32ZM48,128a8,8,0,0,0-8-8H16a8,8,0,0,0,0,16H40A8,8,0,0,0,48,128Zm80,80a8,8,0,0,0-8,8v24a8,8,0,0,0,16,0V216A8,8,0,0,0,128,208Zm112-88H216a8,8,0,0,0,0,16h24a8,8,0,0,0,0-16Z"></path></svg>
      <input type="range" v-model="filterPercentage" min="10" max="100" @input="apply">
    </div>
  </div>
</template>