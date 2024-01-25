<script setup lang="ts">
import { defineProps } from "vue";

defineProps({
  apps: {
    type: Array,
    required: true,
  },
});
function z(app: any) {
  const target = document.getElementById(app);
  if (target) {
    if (target.style.display === "block") {
      target.style.display = "none";
    } else {
      target.style.display = "block";
    }
  }
}
</script>
<template>
  <div
    class="flex gap-3 p-3 fixed bottom-3 left-1/2 -translate-x-1/2 bg-slate-700/50 rounded-2xl shadow-lg border border-slate-400/50"
  >
    <div v-for="app in apps">
      <div v-on:click="z(app)">
        <button class="p-3 bg-slate-800/50 border border-slate-600 rounded-lg transition-all hover:-translate-y-0.5">
          {{ app }}
        </button>
      </div>
    </div>
  </div>
</template>
