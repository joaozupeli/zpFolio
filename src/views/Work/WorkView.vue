<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const svgContainer = ref<HTMLElement | null>(null)

onMounted(() => {
  gsap.from('#work .section-label', {
    scrollTrigger: {
      trigger: '#work',
      start: 'top 80%',
      toggleActions: 'play none none reverse',
    },
    y: 20,
    opacity: 0,
    duration: 0.6,
    ease: 'power4.out',
  })

  gsap.from('#work .page-title', {
    scrollTrigger: {
      trigger: '#work',
      start: 'top 75%',
      toggleActions: 'play none none reverse',
    },
    y: 80,
    opacity: 0,
    duration: 1,
    ease: 'power4.out',
  })

  gsap.from('#work .project-item', {
    scrollTrigger: {
      trigger: '#work .projects-grid',
      start: 'top 80%',
      toggleActions: 'play none none reverse',
    },
    y: 60,
    opacity: 0,
    duration: 0.8,
    stagger: 0.12,
    ease: 'power4.out',
  })

  // Architecture diagram animation
  const archTl = gsap.timeline({
    scrollTrigger: {
      trigger: '#work .architecture',
      start: 'top 80%',
      toggleActions: 'play none none reverse',
    },
  })

  archTl
    .from('#work .arch-title', {
      y: 30,
      opacity: 0,
      duration: 0.6,
      ease: 'power4.out',
    })
    .from(
      '#work .arch-node',
      {
        scale: 0,
        opacity: 0,
        duration: 0.5,
        stagger: 0.1,
        ease: 'back.out(1.7)',
      },
      '-=0.3',
    )
    .from(
      '#work .arch-line',
      {
        scaleX: 0,
        opacity: 0,
        duration: 0.4,
        stagger: 0.08,
        ease: 'power2.out',
        transformOrigin: 'left center',
      },
      '-=0.3',
    )
    .from(
      '#work .arch-line-v',
      {
        scaleY: 0,
        opacity: 0,
        duration: 0.4,
        stagger: 0.08,
        ease: 'power2.out',
        transformOrigin: 'top center',
      },
      '-=0.4',
    )
})
</script>

<template>
  <section id="work" class="work-section">
    <span class="section-label">01 / Work</span>
    <h2 class="page-title">Projects</h2>
    <div class="projects-grid">
      <div class="project-item">
        <div class="project-number">01</div>
        <div class="project-info">
          <h3 class="project-name">Coming soon</h3>
          <span class="project-tag">Microservices & API</span>
        </div>
      </div>
      <div class="project-item">
        <div class="project-number">02</div>
        <div class="project-info">
          <h3 class="project-name">Coming soon</h3>
          <span class="project-tag">Cloud Infrastructure</span>
        </div>
      </div>
      <div class="project-item">
        <div class="project-number">03</div>
        <div class="project-info">
          <h3 class="project-name">Coming soon</h3>
          <span class="project-tag">Full-stack Application</span>
        </div>
      </div>
    </div>

    <div ref="svgContainer" class="architecture">
      <h3 class="arch-title">How I structure a Microservice</h3>
      <div class="arch-diagram">
        <svg viewBox="0 0 700 320" fill="none" xmlns="http://www.w3.org/2000/svg">
          <!-- Client -->
          <rect class="arch-node" x="280" y="10" width="140" height="44" rx="8" stroke="#646cff" stroke-width="1.5" fill="rgba(100,108,255,0.08)" />
          <text x="350" y="37" text-anchor="middle" fill="#fff" font-size="13" font-family="Inter, sans-serif" font-weight="400">Client</text>

          <!-- Line down from Client to API Gateway -->
          <line class="arch-line-v" x1="350" y1="54" x2="350" y2="90" stroke="rgba(255,255,255,0.12)" stroke-width="1.5" />

          <!-- API Gateway -->
          <rect class="arch-node" x="260" y="90" width="180" height="44" rx="8" stroke="#646cff" stroke-width="1.5" fill="rgba(100,108,255,0.08)" />
          <text x="350" y="117" text-anchor="middle" fill="#646cff" font-size="13" font-family="Inter, sans-serif" font-weight="500">API Gateway</text>

          <!-- Lines from Gateway to Services -->
          <line class="arch-line-v" x1="150" y1="134" x2="150" y2="180" stroke="rgba(255,255,255,0.12)" stroke-width="1.5" />
          <line class="arch-line-v" x1="350" y1="134" x2="350" y2="180" stroke="rgba(255,255,255,0.12)" stroke-width="1.5" />
          <line class="arch-line-v" x1="550" y1="134" x2="550" y2="180" stroke="rgba(255,255,255,0.12)" stroke-width="1.5" />

          <!-- Horizontal line connecting services to gateway -->
          <line class="arch-line" x1="150" y1="134" x2="550" y2="134" stroke="rgba(255,255,255,0.12)" stroke-width="1.5" />

          <!-- Auth Service -->
          <rect class="arch-node" x="70" y="180" width="160" height="44" rx="8" stroke="rgba(255,255,255,0.15)" stroke-width="1" fill="rgba(255,255,255,0.03)" />
          <text x="150" y="207" text-anchor="middle" fill="rgba(255,255,255,0.7)" font-size="12" font-family="Inter, sans-serif" font-weight="300">Auth Service</text>

          <!-- Core Service -->
          <rect class="arch-node" x="270" y="180" width="160" height="44" rx="8" stroke="rgba(255,255,255,0.15)" stroke-width="1" fill="rgba(255,255,255,0.03)" />
          <text x="350" y="207" text-anchor="middle" fill="rgba(255,255,255,0.7)" font-size="12" font-family="Inter, sans-serif" font-weight="300">Core Service</text>

          <!-- Notification Service -->
          <rect class="arch-node" x="470" y="180" width="160" height="44" rx="8" stroke="rgba(255,255,255,0.15)" stroke-width="1" fill="rgba(255,255,255,0.03)" />
          <text x="550" y="207" text-anchor="middle" fill="rgba(255,255,255,0.7)" font-size="12" font-family="Inter, sans-serif" font-weight="300">Notification Svc</text>

          <!-- Lines from Services to Databases -->
          <line class="arch-line-v" x1="150" y1="224" x2="150" y2="264" stroke="rgba(255,255,255,0.08)" stroke-width="1" />
          <line class="arch-line-v" x1="350" y1="224" x2="350" y2="264" stroke="rgba(255,255,255,0.08)" stroke-width="1" />
          <line class="arch-line-v" x1="550" y1="224" x2="550" y2="264" stroke="rgba(255,255,255,0.08)" stroke-width="1" />

          <!-- DB nodes -->
          <rect class="arch-node" x="90" y="264" width="120" height="36" rx="6" stroke="rgba(255,255,255,0.1)" stroke-width="1" fill="rgba(255,255,255,0.02)" />
          <text x="150" y="287" text-anchor="middle" fill="rgba(255,255,255,0.4)" font-size="11" font-family="Inter, sans-serif" font-weight="300">Auth DB</text>

          <rect class="arch-node" x="290" y="264" width="120" height="36" rx="6" stroke="rgba(255,255,255,0.1)" stroke-width="1" fill="rgba(255,255,255,0.02)" />
          <text x="350" y="287" text-anchor="middle" fill="rgba(255,255,255,0.4)" font-size="11" font-family="Inter, sans-serif" font-weight="300">Main DB</text>

          <rect class="arch-node" x="490" y="264" width="120" height="36" rx="6" stroke="rgba(255,255,255,0.1)" stroke-width="1" fill="rgba(255,255,255,0.02)" />
          <text x="550" y="287" text-anchor="middle" fill="rgba(255,255,255,0.4)" font-size="11" font-family="Inter, sans-serif" font-weight="300">Queue / MQ</text>
        </svg>
      </div>
    </div>
  </section>
</template>

<style scoped>
.work-section {
  min-height: 100vh;
  padding: 8rem 3rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.section-label {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.3);
  letter-spacing: 0.2em;
  text-transform: uppercase;
  margin-bottom: 1.5rem;
  font-weight: 400;
}

.page-title {
  font-size: clamp(2.5rem, 6vw, 5rem);
  font-weight: 700;
  color: #fff;
  letter-spacing: -0.03em;
  margin: 0 0 4rem;
}

.projects-grid {
  display: flex;
  flex-direction: column;
}

.project-item {
  display: flex;
  align-items: center;
  gap: 2rem;
  padding: 2.5rem 0;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  cursor: pointer;
  transition: opacity 0.3s ease;
}

.project-item:last-child {
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.project-item:hover {
  opacity: 0.6;
}

.project-number {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.3);
  font-weight: 300;
  min-width: 40px;
}

.project-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex: 1;
}

.project-name {
  font-size: clamp(1.5rem, 3vw, 2.5rem);
  font-weight: 500;
  color: #fff;
  margin: 0;
  letter-spacing: -0.02em;
}

.project-tag {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.4);
  font-weight: 300;
}

.architecture {
  margin-top: 6rem;
}

.arch-title {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.4);
  letter-spacing: 0.15em;
  text-transform: uppercase;
  font-weight: 400;
  margin: 0 0 2rem;
}

.arch-diagram {
  max-width: 700px;
}

.arch-diagram svg {
  width: 100%;
  height: auto;
}
</style>
