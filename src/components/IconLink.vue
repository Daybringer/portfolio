<template>
  <a 
    v-bind="$attrs"
    class="stroke-white hover:opacity-70 cursor-pointer p-1 transition-opacity duration-200"
  >
    <slot></slot>
  </a>
</template>

<script setup>
defineOptions({
  inheritAttrs: false
})
</script>