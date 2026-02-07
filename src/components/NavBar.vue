<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const nav = ref<HTMLElement | null>(null)
const activeSection = ref('home')

const sections = ['home', 'work', 'about', 'contact']

function scrollTo(id: string) {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}

onMounted(() => {
  gsap.from(nav.value, {
    y: -40,
    opacity: 0,
    duration: 1,
    ease: 'power3.out',
    delay: 0.5,
  })

  sections.forEach((id) => {
    ScrollTrigger.create({
      trigger: `#${id}`,
      start: 'top center',
      end: 'bottom center',
      onEnter: () => (activeSection.value = id),
      onEnterBack: () => (activeSection.value = id),
    })
  })
})
</script>

<template>
  <nav ref="nav" class="navbar">
    <a class="nav-logo" @click.prevent="scrollTo('home')">João Zupeli</a>
    <div class="nav-links">
      <a
        v-for="section in ['work', 'about', 'contact']"
        :key="section"
        :class="{ active: activeSection === section }"
        @click.prevent="scrollTo(section)"
      >
        {{ section }}
      </a>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2rem 3rem;
  z-index: 100;
  mix-blend-mode: difference;
}

.nav-logo {
  font-size: 1.4rem;
  font-weight: 700;
  color: #fff;
  text-decoration: none;
  letter-spacing: -0.02em;
  cursor: pointer;
}

.nav-links {
  display: flex;
  gap: 2.5rem;
}

.nav-links a {
  color: #fff;
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 400;
  letter-spacing: 0.02em;
  transition: opacity 0.3s ease;
  cursor: pointer;
}

.nav-links a:hover {
  opacity: 0.5;
}

.nav-links a.active {
  opacity: 0.5;
}
</style>
