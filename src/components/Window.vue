<script setup lang="ts">
import { defineProps, ref } from "vue";

defineProps({
  top: {
    type: String,
    required: true,
  },
  left: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
});

const hold = ref<HTMLElement | null>(null);
const container = ref<HTMLElement | null>(null);

let initalX: number = 0;
let initalY: number = 0;
let initMouseX: number = 0;
let initMouseY: number = 0;
let expanded: boolean = false;
let hidden: boolean = false;
let oldWidth = "";
let oldHeight = "";
let oldTop = "";
let oldLeft = "";

function z() {
  const elements = document.getElementsByClassName(
    "resize"
  ) as HTMLCollectionOf<HTMLElement>;
  for (let i = 0; i < elements.length; i++) {
    elements[i].style.zIndex = "2";
    elements[i].classList.remove("ring");
  }
  if (container.value) {
    container.value.style.zIndex = "100";
    container.value.classList.add("ring");
  }
}

function startDrag(event: MouseEvent): void {
  z();
  event.preventDefault();
  if (container.value) {
    initalX = container.value.offsetLeft;
    initalY = container.value.offsetTop;
    initMouseX = event.clientX - container.value.offsetLeft;
    initMouseY = event.clientY - container.value.offsetTop;

    window.addEventListener("mousemove", move);
    window.addEventListener("mouseup", stopMove);
  }
}

function move(event: MouseEvent): void {
  const deltaX = event.clientX - initalX;
  const deltaY = event.clientY - initalY;
  if (container.value) {
    container.value.style.left = initalX + deltaX - initMouseX + "px";
    container.value.style.top = initalY + deltaY - initMouseY + "px";
  }
}

function stopMove(): void {
  window.removeEventListener("mousemove", move);
  window.removeEventListener("mouseup", stopMove);
}
function hide() {
  if (container.value) {
    if (hidden === false) {
      container.value.style.display = "none";
    } else if (hidden === true) {
      container.value.style.display = "block";
    }
  }
}

function toggleExpand() {
  if (container.value) {
    if (expanded === false) {
      oldWidth = container.value.offsetWidth + "px";
      oldHeight = container.value.offsetHeight + "px";
      oldTop = container.value.offsetTop + "px";
      oldLeft = container.value.offsetLeft + "px";
      container.value.style.left = "1rem";
      container.value.style.top = "4rem";
      container.value.style.height = "calc(100% - 5rem)";
      container.value.style.width = "calc(100% - 2rem)";
    } else if (expanded === true) {
      container.value.style.height = oldHeight;
      container.value.style.width = oldWidth;
      container.value.style.left = oldLeft;
      container.value.style.top = oldTop;
    }
    expanded = !expanded;
  }
}
</script>
<template>
  <div
    v-on:click="z"
    class="resize overflow-auto rounded-md shadow-lg fixed h-40 w-80 ring-slate-300"
    ref="container"
    :style="{ top, left }"
  >
    <div v-on:mousedown="startDrag" class="p-2 bg-slate-500/40 backdrop-blur sticky top-0" ref="hold">
      <div class="flex items-center justify-between cursor-move">
        <span class="select-none" :innerHTML="title"></span>
        <div class="flex gap-3">
          <button v-on:click="toggleExpand" class="hover:text-teal-300">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="26"
              height="26"
              fill="currentColor"
              viewBox="0 0 256 256"
            >
              <path
                d="M216,48V88a8,8,0,0,1-16,0V56H168a8,8,0,0,1,0-16h40A8,8,0,0,1,216,48ZM88,200H56V168a8,8,0,0,0-16,0v40a8,8,0,0,0,8,8H88a8,8,0,0,0,0-16Zm120-40a8,8,0,0,0-8,8v32H168a8,8,0,0,0,0,16h40a8,8,0,0,0,8-8V168A8,8,0,0,0,208,160ZM88,40H48a8,8,0,0,0-8,8V88a8,8,0,0,0,16,0V56H88a8,8,0,0,0,0-16Z"
              ></path>
            </svg>
          </button>
          <button v-on:click="hide" class="hover:text-red-300">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="26"
              height="26"
              fill="currentColor"
              viewBox="0 0 256 256"
            >
              <path
                d="M165.66,101.66,139.31,128l26.35,26.34a8,8,0,0,1-11.32,11.32L128,139.31l-26.34,26.35a8,8,0,0,1-11.32-11.32L116.69,128,90.34,101.66a8,8,0,0,1,11.32-11.32L128,116.69l26.34-26.35a8,8,0,0,1,11.32,11.32ZM232,128A104,104,0,1,1,128,24,104.11,104.11,0,0,1,232,128Zm-16,0a88,88,0,1,0-88,88A88.1,88.1,0,0,0,216,128Z"
              ></path>
            </svg>
          </button>
        </div>
      </div>
    </div>
    <div class="p-0 bg-zinc-800 h-full">
      <slot></slot>
    </div>
  </div>
</template>
