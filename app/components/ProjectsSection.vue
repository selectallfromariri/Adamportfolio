<script lang="ts" setup>
import { ref } from 'vue'
import { ArrowLeft, ArrowRight } from '@element-plus/icons-vue'

interface Project {
  id: string
  title: string
  badge?: string
  medal?: string
  image: string
  description: string
  brief: string
  tags: string[]
  github?: string
  media: string[]
  featured?: boolean
}

const projects: Project[] = [
  {
    id: 'wedding',
    title: 'Wedding Management System',
    image: '/assets/images/Wedding Management.png',
    description: 'Wedding Management System where couples manage their wedding digitally and guests RSVP online, with a photo dump feature.',
    brief: 'A digital RSVP and wedding planning hub for couples. Features guest list management, real-time RSVP tracking, digital invitation landing pages, and a collaborative photo gallery where guests can upload memories.',
    tags: ['Nuxt.js', 'Laravel', 'PostgreSQL'],
    github: 'https://github.com/selectallfromariri/Wedd',
    media: ['/assets/images/Wedding Management.png', '/assets/images/Invite.png', '/assets/images/RSVP.png']
  },
  {
    id: 'trackback',
    title: 'TrackBack : Web Based System',
    image: '/assets/images/TrackbackPTA.png',
    description: 'TrackBack is a web-based system designed to help individuals find their lost items with a report lost & found feature.',
    brief: 'Developed as a final year Diploma project, TrackBack is a community-driven web app to report and trace lost items. It uses OpenStreetAPI geolocation to pin where items were lost or found, and PHPMailer to notify owners when matching items are discovered.',
    tags: ['PHP', 'Javascript', 'MySQL', 'OpenStreetAPI', 'PHPMailer'],
    media: ['/assets/images/TrackbackPTA.png', '/assets/images/TrackbackSecond.png']
  },
  {
    id: 'pokedex',
    title: 'Pokedex',
    image: '/assets/images/pokedex.jpeg',
    description: 'A Pokedex application that lets users search for Pokemon and view their stats. Built to learn React Native.',
    brief: 'A personal learning project to master cross-platform mobile development with React Native. Fetches stats, types, and sprites from PokeAPI and displays them in a clean card layout with search and filter.',
    tags: ['React Native', 'PokeAPI'],
    github: 'https://github.com/selectallfromariri/Pokedex',
    media: ['/assets/images/pokedex.jpeg']
  },
  {
    id: 'jimat2go',
    title: 'Jimat2Go',
    medal: 'Hackathon Finalist',
    image: '/assets/images/Jimat2Go.png',
    description: 'Jimat2Go is an AI camera app that intercepts impulse spending in real time.',
    brief: 'Jimat2Go is an AI camera app that I built during BeU by Bank Islam × UMPSA Hackathon X Fintech Forward 2026. It intercepts impulse spending in real time. Point your phone at any product, and it identifies the item, estimates the market price, coaches you on whether you actually need it, suggests where to get it cheaper if you do, and shows what that money could grow into if you dont.',
    tags: ['Flutter', 'FastAPI', 'Gemini AI', 'SerpAPI', 'PostgreSQL'],
    github: 'https://github.com/Jimat2go',
    media: ['/assets/images/Jimat2Go.png', '/assets/images/ScanExample.png', '/assets/images/Exampleoutpu.png']
  },
  {
    id: 'Cynosure',
    title: 'Cynosure.dev',
    medal: 'Freelance Work',
    image: '/assets/images/cynoimg.jpeg',
    description: 'A modern digital solutions platform designed to help businesses attract more customers and streamline their operations.',
    brief: 'Cynosure.dev is a digital solutions company that provides website development, custom business systems, SEO optimization, and digital strategy services for small businesses. As a freelance developer, I designed and developed a modern, responsive website that showcases the company\'s services, reinforces its brand identity, and provides a seamless user experience. The goal was to create a professional online presence that builds credibility and encourages potential clients to get in touch.',
    tags: ['Nuxt.js', 'Vue.js', 'Vue Library', 'Vue Components'],
    media: ['/assets/images/cynosureMain.png', '/assets/images/CynosureCall.png']
  }
]

const activeProject = ref<Project | null>(null)
const currentMediaIndex = ref(0)
const rowRef = ref<HTMLElement | null>(null)

function scrollCards(dir: 'left' | 'right') {
  rowRef.value?.scrollBy({ left: dir === 'right' ? 310 : -310, behavior: 'smooth' })
}

function openProject(project: Project) {
  activeProject.value = project
  currentMediaIndex.value = 0
  if (typeof document !== 'undefined') document.body.style.overflow = 'hidden'
}

function closeModal() {
  activeProject.value = null
  if (typeof document !== 'undefined') document.body.style.overflow = ''
}

function nextMedia() {
  if (!activeProject.value) return
  currentMediaIndex.value = (currentMediaIndex.value + 1) % activeProject.value.media.length
}

function prevMedia() {
  if (!activeProject.value) return
  const len = activeProject.value.media.length
  currentMediaIndex.value = (currentMediaIndex.value - 1 + len) % len
}
</script>

<template>
  <section id="projects" class="section projects-section">
    <div class="container">

      <!-- Header -->
      <div class="projects-header">
        <div>
          <p class="section-label">Projects</p>
          <h2 class="font-display section-title">Things I've built.</h2>
        </div>
        <p class="projects-subtitle">A selection of projects I'm proud of.</p>
      </div>

      <!-- ── Projects carousel with arrow buttons ── -->
      <div class="carousel-wrapper">
        <!-- Left arrow -->
        <el-button
          class="scroll-arrow scroll-arrow--left"
          circle
          @click="scrollCards('left')"
        >
          <el-icon><ArrowLeft /></el-icon>
        </el-button>

        <!-- Scrollable row -->
        <div ref="rowRef" class="projects-row">
          <div
            v-for="project in projects"
            :key="project.id"
            class="card project-card"
            @click="openProject(project)"
          >
            <!-- Featured pill -->
            <div v-if="project.badge" class="badge-pill badge-gray card-badge">{{ project.badge }}</div>
            <!-- Hackathon medal -->
            <div v-if="project.medal" class="badge-pill badge-black medal">{{ project.medal }}</div>

            <el-image :src="project.image" class="card-img" fit="cover" />
            <h3 class="project-title font-display">{{ project.title }}</h3>
            <p class="project-desc">{{ project.description }}</p>
            <div class="project-tags">
              <span v-for="tag in project.tags" :key="tag" class="skill-pill">{{ tag }}</span>
            </div>
            <div v-if="project.github" class="project-links" @click.stop>
              <a :href="project.github" target="_blank" rel="noopener" class="btn-black">View on GitHub</a>
            </div>
          </div>
        </div>

        <!-- Right arrow -->
        <el-button
          class="scroll-arrow scroll-arrow--right"
          circle
          @click="scrollCards('right')"
        >
          <el-icon><ArrowRight /></el-icon>
        </el-button>
      </div>

      <p class="more-soon">· · · more coming soon</p>
    </div>

    <!-- ── Detail Modal ── -->
    <Transition name="modal-fade">
      <div v-if="activeProject" class="modal-overlay" @click.self="closeModal">
        <div class="modal-card">
          <button class="modal-close" @click="closeModal">×</button>
          <div class="modal-body">

            <!-- Left: media carousel -->
            <div class="modal-media">
              <div class="carousel-frame">
                <el-image
                  v-if="activeProject.media[currentMediaIndex] !== 'no image'"
                  :src="activeProject.media[currentMediaIndex]"
                  fit="cover"
                  class="carousel-img"
                />
                <div v-else class="no-img-text">No image provided yet</div>
              </div>
              <div v-if="activeProject.media.length > 1" class="carousel-controls">
                <button class="carousel-btn" @click="prevMedia">←</button>
                <div class="dot-row">
                  <span
                    v-for="(_, i) in activeProject.media"
                    :key="i"
                    class="dot"
                    :class="{ 'dot--on': i === currentMediaIndex }"
                    @click="currentMediaIndex = i"
                  />
                </div>
                <button class="carousel-btn" @click="nextMedia">→</button>
              </div>
            </div>

            <!-- Right: details -->
            <div class="modal-details">
              <div class="modal-badges">
                <span v-if="activeProject.badge" class="badge-pill badge-gray">{{ activeProject.badge }}</span>
                <span v-if="activeProject.medal" class="badge-pill badge-black">{{ activeProject.medal }}</span>
              </div>
              <h3 class="modal-title font-display">{{ activeProject.title }}</h3>
              <p class="modal-brief">{{ activeProject.brief }}</p>
              <div class="project-tags">
                <span v-for="tag in activeProject.tags" :key="tag" class="skill-pill">{{ tag }}</span>
              </div>
              <div v-if="activeProject.github" class="project-links">
                <a :href="activeProject.github" target="_blank" rel="noopener" class="btn-black">View on GitHub</a>
              </div>
            </div>

          </div>
        </div>
      </div>
    </Transition>
  </section>
</template>

<style scoped>
/* ── Section ── */
.projects-section {
  background: rgba(255, 255, 255, 0.88);
}
@media (max-width: 768px) {
  .projects-section { background-color: #fff; border-top: 1px solid #e5e5e5; }
}

/* ── Header ── */
.projects-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 48px;
  gap: 32px;
  flex-wrap: wrap;
}
.section-label {
  font-size: 0.875rem;
  font-weight: 400;
  color: #737373;
  margin: 0 0 12px;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}
.section-title {
  font-size: 2.25rem;
  font-weight: 500;
  color: #000;
  line-height: 1.15;
  margin: 0;
  letter-spacing: -0.02em;
}
.projects-subtitle {
  font-size: 1rem;
  color: #737373;
  line-height: 1.6;
  margin: auto 0 0;
  max-width: 280px;
}

/* ── Shared badge pill ── */
.badge-pill {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-size: 0.75rem;
  font-weight: 500;
  border-radius: 9999px;
  padding: 4px 14px;
  text-transform: uppercase;
  letter-spacing: 0.07em;
  white-space: nowrap;
}
.badge-gray {
  color: #262626;
  background: #e5e5e5;
  border: 1px solid #e5e5e5;
}
.badge-black {
  color: #fff;
  background: #000;
  border: 1px solid #000;
}

/* ── Carousel wrapper: positions arrows on each side ── */
.carousel-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  gap: 12px;
}

/* ── Scroll arrow buttons ── */
.scroll-arrow {
  flex-shrink: 0;
  background: #fff !important;
  border: 1px solid #e5e5e5 !important;
  color: #262626 !important;
  width: 38px !important;
  height: 38px !important;
  box-shadow: none !important;
  transition: border-color 0.15s !important;
}
.scroll-arrow:hover {
  border-color: #a3a3a3 !important;
}

/* ── Projects row — hidden scrollbar ── */
.projects-row {
  display: flex;
  flex-wrap: nowrap;
  gap: 20px;
  overflow-x: auto;
  scroll-behavior: smooth;
  padding-top: 16px; /* prevent absolute medal badge from getting cut off */
  /* hide scrollbar cross-browser */
  -ms-overflow-style: none;
  scrollbar-width: none;
}
.projects-row::-webkit-scrollbar {
  display: none;
}

/* ── Project card ── */
.project-card {
  flex: 0 0 280px;          /* fixed 280px wide, never shrink */
  display: flex;
  flex-direction: column;
  gap: 14px;
  position: relative;
  cursor: pointer;
  transition: border-color 0.15s;
}
.project-card:hover { border-color: #a3a3a3; }

/* Inline badge inside card (e.g. Featured) */
.card-badge {
  align-self: flex-start;
  margin-bottom: 4px;
}

.card-img {
  width: 100%;
  aspect-ratio: 16 / 7;
  border-radius: 8px;
  border: 1px solid #e5e5e5;
  background: #fafafa;
  display: block;
  overflow: hidden;
}

/* Medal — sits on top of card border */
.medal {
  position: absolute;
  top: -13px;
  left: 20px;
  z-index: 5;
  box-shadow: 0 0 0 2px #fff;
}

/* ── Shared card text ── */
.project-title {
  font-size: 1.2rem;
  font-weight: 500;
  color: #000;
  margin: 0;
  letter-spacing: -0.01em;
}
.project-desc {
  font-size: 0.9375rem;
  color: #737373;
  line-height: 1.6;
  margin: 0;
  flex: 1;
}
.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}
.project-links {
  display: flex;
  gap: 10px;
  margin-top: auto;
  flex-wrap: wrap;
  padding-top: 4px;
}

/* ── Modal overlay ── */
.modal-overlay {
  position: fixed;
  inset: 0;
  z-index: 1000;
  background: rgba(0, 0, 0, 0.45);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

/* ── Modal card ── */
.modal-card {
  position: relative;
  background: #fff;
  border: 1px solid #e5e5e5;
  border-radius: 12px;
  width: 100%;
  max-width: 860px;
  max-height: 88vh;
  padding: 36px 32px 32px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
.modal-close {
  position: absolute;
  top: 14px;
  right: 18px;
  background: none;
  border: none;
  font-size: 1.8rem;
  line-height: 1;
  color: #737373;
  cursor: pointer;
  padding: 0;
}
.modal-close:hover { color: #000; }

/* ── Modal inner flex ── */
.modal-body {
  display: flex;
  gap: 32px;
  overflow: hidden;
  flex: 1;
}
.modal-media {
  flex: 1.2;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 14px;
  min-width: 0;
}
.modal-details {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 16px;
  overflow-y: auto;
  min-width: 0;
}
.modal-badges { display: flex; gap: 8px; flex-wrap: wrap; }
.modal-title {
  font-size: 1.6rem;
  font-weight: 500;
  color: #000;
  margin: 0;
  line-height: 1.2;
}
.modal-brief {
  font-size: 0.9375rem;
  color: #525252;
  line-height: 1.65;
  margin: 0;
  flex: 1;
}

/* ── Carousel ── */
.carousel-frame {
  width: 100%;
  aspect-ratio: 16 / 10;
  border-radius: 8px;
  border: 1px solid #e5e5e5;
  background: #fafafa;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}
.carousel-img { width: 100%; height: 100%; }
.no-img-text { font-size: 0.875rem; color: #a3a3a3; }

.carousel-controls {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.carousel-btn {
  background: #e5e5e5;
  border: 1px solid #e5e5e5;
  border-radius: 9999px;
  width: 32px;
  height: 32px;
  cursor: pointer;
  font-size: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
}
.carousel-btn:hover { background: #d4d4d4; }
.dot-row { display: flex; gap: 6px; }
.dot {
  width: 8px;
  height: 8px;
  border-radius: 9999px;
  background: #e5e5e5;
  cursor: pointer;
}
.dot--on { background: #000; }

/* ── Transition ── */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.2s ease, transform 0.2s ease;
}
.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
  transform: scale(0.96);
}

/* ── Responsive ── */
@media (max-width: 767px) {
  .scroll-arrow { display: none !important; }
  .projects-row { flex-direction: column; overflow-x: visible; }
  .project-card { flex: 1 1 100%; min-width: 100%; }
  .section-title { font-size: 1.75rem; }
  .projects-subtitle { max-width: 100%; }
  .modal-body { flex-direction: column; overflow-y: auto; }
  .modal-card { padding: 24px 18px 20px; max-height: 92vh; }
}

/* ── Footer text ── */
.more-soon {
  text-align: center;
  font-size: 0.875rem;
  color: #a3a3a3;
  margin: 32px 0 0;
  letter-spacing: 0.08em;
}
</style>
