<template>
  <div class="relative w-full h-64 rounded overflow-hidden bg-zinc-700">
    <div class="relative w-full h-full">
      <img 
        v-for="(image, index) in images" 
        :key="index"
        :src="image.src" 
        :alt="image.alt || `${projectName} screenshot ${index + 1}`"
        :class="[
          'absolute inset-0 w-full h-full object-contain transition-opacity duration-500',
          index === currentIndex ? 'opacity-100' : 'opacity-0'
        ]"
      />
      
      <div 
        v-if="!imagesLoaded"
        class="absolute inset-0 flex items-center justify-center bg-zinc-700"
      >
        <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-white"></div>
      </div>
    </div>

    <button 
      v-if="images.length > 1"
      @click="previousImage"
      class="absolute left-2 top-1/2 transform -translate-y-1/2 bg-black bg-opacity-50 hover:bg-opacity-70 text-white cursor-pointer p-2 rounded-full transition-all duration-200 hover:scale-110"
      aria-label="Previous image"
    >
      <ChevronLeftIcon class="w-5 h-5" />
    </button>

    <button 
      v-if="images.length > 1"
      @click="nextImage"
      class="absolute right-2 top-1/2 transform -translate-y-1/2 bg-black bg-opacity-50 hover:bg-opacity-70 text-white p-2 cursor-pointer rounded-full transition-all duration-200 hover:scale-110"
      aria-label="Next image"
    >
      <ChevronRightIcon class="w-5 h-5" />
    </button>

    <div 
      v-if="images.length > 1"
      class="absolute bottom-4 left-1/2 transform -translate-x-1/2 flex space-x-2"
    >
      <button
        v-for="(image, index) in images"
        :key="index"
        @click="currentIndex = index"
        class="cursor-pointer"
        :class="[
          'w-2 h-2 rounded-full transition-all duration-200',
          index === currentIndex 
            ? 'bg-white scale-125' 
            : 'bg-white bg-opacity-50 hover:bg-opacity-75'
        ]"
        :aria-label="`Přejít na obrázek č. ${index + 1}`"
      ></button>
    </div>

    <div 
      v-if="images.length > 1"
      class="absolute top-2 right-2 bg-black bg-opacity-50 text-white px-2 py-1 rounded text-sm"
    >
      {{ currentIndex + 1 }} / {{ images.length }}
    </div>

    <div 
      v-if="showZoom"
      @click="closeZoom"
      class="fixed inset-0 z-50 bg-black bg-opacity-90 flex items-center justify-center p-4"
    >
      <div class="relative max-w-full max-h-full">
        <img 
          :src="images[currentIndex].src" 
          :alt="images[currentIndex].alt"
          class="max-w-full max-h-full object-contain"
        />
        <button 
          @click="closeZoom"
          class="absolute top-4 right-4 text-white bg-black cursor-pointer bg-opacity-50 hover:bg-opacity-70 p-2 rounded-full"
        >
          <XIcon class="w-6 h-6" />
        </button>
      </div>
    </div>

    <button 
      @click="openZoom"
      class="absolute top-2 left-2 bg-black bg-opacity-50 hover:bg-opacity-70 cursor-pointer text-white p-2 rounded-full transition-all duration-200"
      aria-label="Zoom image"
    >
      <ZoomInIcon class="w-4 h-4" />
    </button>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import ChevronLeftIcon from './icons/ChevronLeftIcon.vue'
import ChevronRightIcon from './icons/ChevronRightIcon.vue'
import XIcon from './icons/XIcon.vue'
import ZoomInIcon from './icons/ZoomInIcon.vue'

const props = defineProps({
  images: {
    type: Array,
    required: true,
    validator: (images) => {
      return images.every(img => 
        typeof img === 'object' && 
        typeof img.src === 'string'
      )
    }
  },
  projectName: {
    type: String,
    default: 'Project'
  },
  autoPlay: {
    type: Boolean,
    default: false
  },
  autoPlayInterval: {
    type: Number,
    default: 5000
  }
})

const currentIndex = ref(0)
const imagesLoaded = ref(false)
const showZoom = ref(false)
let autoPlayTimer = null

const nextImage = () => {
  currentIndex.value = (currentIndex.value + 1) % props.images.length
}

const previousImage = () => {
  currentIndex.value = currentIndex.value === 0 
    ? props.images.length - 1 
    : currentIndex.value - 1
}

const openZoom = () => {
  showZoom.value = true
  document.body.style.overflow = 'hidden'
}

const closeZoom = () => {
  showZoom.value = false
  document.body.style.overflow = 'auto'
}

const startAutoPlay = () => {
  if (props.autoPlay && props.images.length > 1) {
    autoPlayTimer = setInterval(nextImage, props.autoPlayInterval)
  }
}

const stopAutoPlay = () => {
  if (autoPlayTimer) {
    clearInterval(autoPlayTimer)
    autoPlayTimer = null
  }
}

const handleKeydown = (event) => {
  if (showZoom.value) {
    if (event.key === 'Escape') {
      closeZoom()
    } else if (event.key === 'ArrowLeft') {
      previousImage()
    } else if (event.key === 'ArrowRight') {
      nextImage()
    }
  }
}

const preloadImages = () => {
  const promises = props.images.map(image => {
    return new Promise((resolve) => {
      const img = new Image()
      img.onload = resolve
      img.onerror = resolve
      img.src = image.src
    })
  })
  
  Promise.all(promises).then(() => {
    imagesLoaded.value = true
  })
}

onMounted(() => {
  preloadImages()
  startAutoPlay()
  document.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  stopAutoPlay()
  document.removeEventListener('keydown', handleKeydown)
  document.body.style.overflow = 'auto'
})
</script>

<style scoped>
.fixed::-webkit-scrollbar {
  display: none;
}

.fixed {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>