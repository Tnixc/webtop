<script setup lang="ts">
import Window from "./components/Window.vue";
import Dock from "./components/Dock.vue";
import TopBar from "./components/TopBar.vue";
</script>
<template>
  <body class="h-screen text-zinc-50">
    <TopBar />
    <Window
      id="About"
      title="About"
      top="80px"
      left="190px"
      class="min-w-48 min-h-48"
    >
      <h1>Hello world 1</h1>
    </Window>
    <Window
      id="Contact"
      title="Contact"
      top="50px"
      left="90px"
      class="min-w-48 min-h-48"
    >
      <h1>Hello world 2</h1>
    </Window>
    <Window
      id="Projects"
      title="Projects"
      top="440px"
      left="1000px"
      class="min-w-48 min-h-48"
    >
      <h1>Hello world 3</h1>
    </Window>
    <Dock :apps="['About', 'Contact', 'Projects']" />
  </body>
</template>
