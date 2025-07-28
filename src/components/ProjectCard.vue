<template>
  <div class="rounded-sm border-white border-4 bg-zinc-900 px-4 md:px-8 py-12 md:py-6 z-auto text-white relative">
    <div class="absolute top-2 right-4 z-0 flex flex-row gap-3">
      <IconLink 
        v-if="webLink"
        :href="webLink" 
        target="_blank"
        title="Visit Website"
      >
        <WebIcon class="h-10 w-10 stroke-slate-100" />
      </IconLink>
      
      <IconLink 
        v-if="gitLink"
        :href="gitLink" 
        target="_blank"
        title="View on GitHub"
      >
        <GitHubIcon class="h-10 w-10 stroke-slate-100" />
      </IconLink>
    </div>
    
    <p class="text-3xl">{{ title }}</p>
    <p class="text-xl font-light mt-1">{{ subtitle }}</p>
    
    <hr class="mb-2 mt-3" />
    
    <div class="flex flex-row gap-x-4 gap-y-1 justify-center flex-wrap">
      <slot name="technologies"></slot>
    </div>
    
    <hr class="mb-2 mt-3" />
    
    <p class="leading-relaxed">
      <slot name="description"></slot>
    </p>
    
    <hr class="my-3" />
    
    <div>
      <ImageCarousel 
        v-if="images && images.length > 0"
        :images="images"
        :project-name="title"
        :auto-play="autoPlay"
      />
      <img 
        v-else-if="image"
        class="rounded w-full h-64 object-cover" 
        :src="image" 
        :alt="title"
      />
    </div>
  </div>
</template>

<script setup>
import IconLink from './IconLink.vue'
import WebIcon from './icons/WebIcon.vue'
import GitHubIcon from './icons/GitHubIcon.vue'
import ImageCarousel from './ImageCarousel.vue'

defineProps({
  title: {
    type: String,
    required: true
  },
  subtitle: {
    type: String,
    required: true
  },
  webLink: {
    type: String,
    default: null
  },
  gitLink: {
    type: String,
    default: null
  },
  image: {
    type: String,
    default: null
  },
  images: {
    type: Array,
    default: () => []
  },
  autoPlay: {
    type: Boolean,
    default: false
  }
})
</script>

<style scoped>
</style>