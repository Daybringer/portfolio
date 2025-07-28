<template>
  <div class="bg-zinc-800 text-white min-h-screen">
    <div class="lines w-full min-h-screen flex justify-center place-items-center relative">
      <div class="w-full flex justify-center md:justify-end absolute top-0 z-20 md:px-12 py-3">
        <div class="flex gap-4 bg-zinc-900 bg-opacity-10 rounded p-2">
          <IconLink 
            href="/cv.pdf" 
            download 
            title="Download CV"
          >
            <CVIcon class="h-10 w-10 stroke-slate-100" />
          </IconLink>
          
          <IconLink 
            href="https://www.linkedin.com/in/michal-va%C5%88ata-670a21127" 
            target="_blank"
            title="LinkedIn Profile"
          >
            <LinkedInIcon class="h-10 w-10 stroke-slate-100" />
          </IconLink>
          
          <IconLink 
            href="https://github.com/Daybringer" 
            target="_blank"
            title="GitHub Profile"
          >
            <GitHubIcon class="h-10 w-10 stroke-slate-100" />
          </IconLink>
        </div>
      </div>

      <AnimatedLines />

      <div class="flex flex-col place-items-center gap-6 rounded-sm border-white border-4 bg-zinc-900 px-12 py-6 md:px-28 md:py-14 z-10 max-w-4xl mx-4">
        <div class="text-center">
          <p class="text-4xl md:text-5xl text-white font-light mb-2">Michal Vaňata</p>
          <p class="text-xl md:text-2xl text-white opacity-90 font-light">Softwarový vývojář</p>
        </div>

        <div class="text-center max-w-2xl">
          <p class="text-white opacity-80 text-base md:text-lg leading-relaxed">
            Specializuji se na moderní webové technologie s důrazem na <span class="text-green-400">Vue.js</span>, 
            <span class="text-green-400">Nuxt</span> a <span class="text-blue-400">TypeScript</span>. 
            Vytvářím interaktivní webové aplikace a mobilní řešení.
          </p>
        </div>

        <div class="flex flex-col md:flex-row gap-4 mt-4">
          <a 
            href="#projects" 
            @click="scrollToProjects"
            class="bg-white text-zinc-900 px-6 py-3 text-center rounded-full font-medium hover:bg-opacity-90 transition-all duration-200 hover:scale-105"
          >
            Zobrazit projekty
          </a>
          <a 
            href="#contact" 
            @click="scrollToContact"
            class="border border-white text-center text-white px-6 py-3 rounded-full font-medium hover:bg-white hover:text-zinc-900 transition-all duration-200"
          >
            Kontakt
          </a>
        </div>
      </div>
    </div>

    <div id="projects" class="flex justify-center text-center flex-col place-items-center gap-12 pb-8 px-4">
      <h3 class="text-4xl text-white">Projekty</h3>
      
      <div class="grid grid-cols-1 md:w-8/12 xl:grid-cols-2 gap-10">
        <ProjectCard
          title="Vylezeno.cz"
          subtitle="Online lezecký deníček a disk. fórum"
          web-link="https://vylezeno.cz/"
          :images="vylezenoImages"
          :auto-play="true"
        >
          <template #technologies>
            <TechBadge>
              <NuxtIcon class="h-10" />
              Nuxt
            </TechBadge>
            <TechBadge>
              <TailwindIcon class="h-10" />
              Tailwind CSS
            </TechBadge>
            <TechBadge>
              <TypeScriptIcon class="h-9" />
              Typescript
            </TechBadge>
            <TechBadge>
              <PocketBaseIcon class="h-8 mr-1" />
              Pocketbase
            </TechBadge>
            <TechBadge>
              <PrimeVueIcon class="h-8 mr-1" />
              Primevue
            </TechBadge>
            <TechBadge>
              <CapacitorIcon class="h-10 mr-1" />
              Capacitor
            </TechBadge>
          </template>
          
          <template #description>
            <strong>VE VÝVOJI</strong><br />
            Vylezeno.cz je web a hybridní mobilní aplikace sloužící jako databáze lezeckých cest a jejich přelezů.<br /><br />
            Mezi další funkce patří diskuzní fórum, krátké články o aktualitách z lezeckého prostředí, komentování cest a přehledy posledních významných přelezů.
          </template>
        </ProjectCard>

        <ProjectCard
          title="Gomoku"
          subtitle="Platforma na hraní piškvorek"
          web-link="https://gomoku.vanata.dev/"
          git-link="https://github.com/Daybringer/gomoku"
          :images="gomokuImages"
        >
          <template #technologies>
            <TechBadge>
              <VueIcon class="h-10" />
              Vue.js
            </TechBadge>
            <TechBadge>
              <TailwindIcon class="h-10" />
              Tailwind CSS
            </TechBadge>
            <TechBadge>
              <TypeScriptIcon class="h-9" />
              Typescript
            </TechBadge>
            <TechBadge>
              <NestJSIcon class="h-8 mr-1" />
              NestJS
            </TechBadge>
            <TechBadge>
              <WebSocketIcon class="h-10" />
              WebSockets
            </TechBadge>
          </template>
          
          <template #description>
            Gomoku je platforma pro online hraní piškvorek proti ostatním hráčům. Nabízí různé funkce, jako je žebříček nejlepších hráčů, lokální hra proti botovi, a upravitelné profily hráčů.<br /><br />
            Uživatelé mohou soutěžit v reálném čase a sledovat svůj postup a úspěchy ve hře.
            <br><br>
          </template>
        </ProjectCard>
      </div>
    </div>

    <div id="contact" class="bg-zinc-900 py-16 px-4">
      <div class="max-w-4xl mx-auto text-center">
        <h3 class="text-4xl text-white mb-8">Spojme se</h3>
        <p class="text-white opacity-80 text-lg mb-8 max-w-2xl mx-auto">
          Hledáte nadšeného vývojáře pro váš projekt? Nebo máte zajímavou nabídku spolupráce? 
          Rád si s vámi promluvím!
        </p>
        
        <div class="flex flex-col md:flex-row gap-6 justify-center items-center">
          <a 
            href="mailto:vanata.michal@gmail.com" 
            class="bg-white text-zinc-900 px-8 py-4 rounded-full font-medium hover:bg-opacity-90 transition-all duration-200 hover:scale-105 flex items-center gap-2"
          >
            <EmailIcon class="w-5 h-5" />
            Napište mi email
          </a>
          
          <div class="flex gap-4">
            <a 
              href="https://www.linkedin.com/in/michal-va%C5%88ata-670a21127" 
              target="_blank"
              class="border border-white text-white p-3 rounded-full hover:bg-white hover:text-zinc-900 transition-all duration-200"
            >
              <LinkedInIcon class="w-6 h-6" />
            </a>
            <a 
              href="https://github.com/Daybringer" 
              target="_blank"
              class="border border-white text-white p-3 rounded-full hover:bg-white hover:text-zinc-900 transition-all duration-200"
            >
              <GitHubIcon class="w-6 h-6" />
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import AnimatedLines from './components/AnimatedLines.vue'
import IconLink from './components/IconLink.vue'
import ProjectCard from './components/ProjectCard.vue'
import TechBadge from './components/TechBadge.vue'
import CVIcon from './components/icons/CVIcon.vue'
import LinkedInIcon from './components/icons/LinkedInIcon.vue'
import GitHubIcon from './components/icons/GitHubIcon.vue'
import NuxtIcon from './components/icons/NuxtIcon.vue'
import TailwindIcon from './components/icons/TailwindIcon.vue'
import TypeScriptIcon from './components/icons/TypeScriptIcon.vue'
import VueIcon from './components/icons/VueIcon.vue'
import NestJSIcon from './components/icons/NestJSIcon.vue'
import WebSocketIcon from './components/icons/WebSocketIcon.vue'
import PocketBaseIcon from './components/icons/PocketBaseIcon.vue'
import PrimeVueIcon from './components/icons/PrimeVueIcon.vue'
import CapacitorIcon from './components/icons/CapacitorIcon.vue'
import EmailIcon from './components/icons/EmailIcon.vue'

const scrollToProjects = (e) => {
  e.preventDefault()
  document.getElementById('projects').scrollIntoView({ 
    behavior: 'smooth' 
  })
}

const scrollToContact = (e) => {
  e.preventDefault()
  document.getElementById('contact').scrollIntoView({ 
    behavior: 'smooth' 
  })
}

const vylezenoImages = [
  { 
    src: '/vylezeno-home.webp', 
    alt: 'Vylezeno.cz - hlavní stránka' 
  },
  { 
    src: '/vylezeno-profile.webp', 
    alt: 'Vylezeno.cz - pohled na profil uživatele' 
  },
  { 
    src: '/vylezeno-route.webp', 
    alt: 'Vylezeno.cz - pohled na jednotlivou cestu' 
  },
]

const gomokuImages = [
  { 
    src: '/gomoku-home.webp', 
    alt: 'Indexová stránka Gomoku' 
  },
  { 
    src: '/gomoku-game2.webp', 
    alt: 'Hra Gomoku se standarním vzhledem' 
  },
  { 
    src: '/gomoku-game1.webp', 
    alt: 'Hra Gomoku s jedním z alternativních vzhledů' 
  },
  { 
    src: '/gomoku-profile.webp', 
    alt: 'Obrázek uživatelského profilu' 
  }
]
</script>