<template>
  <div>
    <div class="line"></div>
    <div class="line"></div>
    <div class="line"></div>
  </div>
</template>

<script setup>
// No script needed for this component
</script>

<style scoped>
.line {
  --tw-bg-opacity: 1;
  background-color: rgb(24 24 27 / var(--tw-bg-opacity));
  height: 100%;
  left: 50%;
  overflow: hidden;
  position: absolute;
  top: 0;
  width: 5px;
}

.line:after {
  animation: drop 7s 0s infinite;
  animation-fill-mode: forwards;
  animation-timing-function: cubic-bezier(0.4, 0.26, 0, 0.97);
  background: linear-gradient(180deg, rgba(255, 255, 255, 0) 0%, #fff 75%, #fff);
  content: "";
  display: block;
  height: 15vh;
  left: 0;
  position: absolute;
  top: -50%;
  width: 100%;
}

.line:first-child {
  margin-left: -25%;
}

.line:first-child:after {
  animation-delay: 2s;
}

.line:nth-child(3) {
  margin-left: 25%;
}

.line:nth-child(3):after {
  animation-delay: 2s;
}

@keyframes drop {
  0% {
    top: -50%;
  }
  100% {
    top: 110%;
  }
}
</style>