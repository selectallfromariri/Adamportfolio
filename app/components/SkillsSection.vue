<template>
  <section id="skills" class="section skills-section">
    <!-- Header (inside container, but marquees are full-width) -->
    <div class="container skills-header">
      <p class="section-label">Skills</p>
      <h2 class="font-display section-title">Technologies I work with.</h2>
      <p class="section-sub">My current stack, but it's always growing.</p>
    </div>

    <!-- Row 1: Frontend — scrolls left -->
    <div class="marquee-wrapper">
      <p class="row-label">Frontend</p>
      <div class="marquee-fade">
        <div class="marquee-track">
          <div class="marquee-content" v-for="n in 10" :key="'f'+n">
            <div v-for="skill in frontend" :key="skill.name + n" class="skill-chip">
              <img :src="skill.icon" :alt="skill.name" class="chip-icon" loading="lazy" />
              <span class="chip-name">{{ skill.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Row 2: Backend & Database — scrolls right -->
    <div class="marquee-wrapper">
      <p class="row-label">Backend &amp; Database</p>
      <div class="marquee-fade">
        <div class="marquee-track reverse">
          <div class="marquee-content" v-for="n in 10" :key="'b'+n">
            <div v-for="skill in backend" :key="skill.name + n" class="skill-chip">
              <img :src="skill.icon" :alt="skill.name" class="chip-icon" loading="lazy" />
              <span class="chip-name">{{ skill.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Row 3: Tools — scrolls left -->
    <div class="marquee-wrapper">
      <p class="row-label">Tools &amp; Workflow</p>
      <div class="marquee-fade">
        <div class="marquee-track">
          <div class="marquee-content" v-for="n in 10" :key="'t'+n">
            <div v-for="skill in tools" :key="skill.name + n" class="skill-chip">
              <img :src="skill.icon" :alt="skill.name" class="chip-icon" loading="lazy" />
              <span class="chip-name">{{ skill.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

  </section>
</template>

<script lang="ts" setup>
const CDN = 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons'

const frontend = [
  { name: 'Vue.js',       icon: `${CDN}/vuejs/vuejs-original.svg` },
  { name: 'Nuxt',         icon: `${CDN}/nuxtjs/nuxtjs-original.svg` },
  { name: 'React',        icon: `${CDN}/react/react-original.svg` },
  { name: 'React Native', icon: `${CDN}/react/react-original.svg` },
  { name: 'Tailwind CSS', icon: `${CDN}/tailwindcss/tailwindcss-original.svg` },
  { name: 'TypeScript',   icon: `${CDN}/typescript/typescript-original.svg` },
  { name: 'JavaScript',   icon: `${CDN}/javascript/javascript-original.svg` },
]

const backend = [
  { name: 'Laravel',    icon: `${CDN}/laravel/laravel-original.svg` },
  { name: 'PHP',        icon: `${CDN}/php/php-original.svg` },
  { name: 'PostgreSQL', icon: `${CDN}/postgresql/postgresql-original.svg` },
  { name: 'MySQL',      icon: `${CDN}/mysql/mysql-original.svg` },
]

const tools = [
  { name: 'Git',     icon: `${CDN}/git/git-original.svg` },
  { name: 'GitHub',  icon: `${CDN}/github/github-original.svg` },
  { name: 'VS Code', icon: `${CDN}/vscode/vscode-original.svg` },
  { name: 'Figma',   icon: `${CDN}/figma/figma-original.svg` },
  { name: 'Postman', icon: `${CDN}/postman/postman-original.svg` },
]
</script>

<style scoped>
/* ── Section shell ── */
.skills-section {
  background-color: transparent;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 0;
  padding-top: 80px;
  padding-bottom: 80px;
}


@media (max-width: 768px) {
  .skills-section {
    background-color: #fafafa;
    border-top: 1px solid #e5e5e5;
  }
}

.skills-header {
  margin-bottom: 52px;
  text-align: center;
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
  color: #000000;
  line-height: 1.15;
  margin: 0 0 10px;
  letter-spacing: -0.02em;
}

.section-sub {
  font-size: 1rem;
  color: #737373;
  margin: 0;
}

/* ── Marquee rows ── */
.marquee-wrapper {
  margin-bottom: 24px;
}

.row-label {
  font-size: 0.75rem;
  font-weight: 500;
  color: #a3a3a3;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin: 0 0 10px 0;
  text-align: center;
}

/* Fade edges */
.marquee-fade {
  position: relative;
  overflow: hidden;
}
.marquee-fade::before,
.marquee-fade::after {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  width: 80px;
  z-index: 2;
  pointer-events: none;
}
.marquee-fade::before {
  left: 0;
  background: linear-gradient(to right, rgba(250, 250, 250, 0.88), transparent);
}
.marquee-fade::after {
  right: 0;
  background: linear-gradient(to left, rgba(250, 250, 250, 0.88), transparent);
}

@media (max-width: 768px) {
  .marquee-fade::before {
    background: linear-gradient(to right, #fafafa, transparent);
  }
  .marquee-fade::after {
    background: linear-gradient(to left, #fafafa, transparent);
  }
}

/* The track — multi-reps to loop seamlessly */
.marquee-track {
  display: flex;
  width: max-content;
  gap: 24px; /* Big gap between the sets */
  animation: marquee-left 60s linear infinite;
}
.marquee-track.reverse {
  animation: marquee-right 60s linear infinite;
}
.marquee-track:hover,
.marquee-track.reverse:hover {
  animation-play-state: paused;
}

/* Duplicated content side by side */
.marquee-content {
  display: flex;
  gap: 20px; /* Gap between individual skill chips */
  flex-shrink: 0;
}

/* ── Skill chip ── */
.skill-chip {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  background: #ffffff;
  border: 1px solid #e5e5e5;
  border-radius: 12px;
  padding: 12px 20px;
  white-space: nowrap;
  flex-shrink: 0;
  transition: transform 0.2s ease, border-color 0.2s ease;
}

.skill-chip:hover {
  transform: translateY(-2px);
  border-color: #d4d4d4;
}

.chip-icon {
  width: 24px;
  height: 24px;
  object-fit: contain;
  display: block;
}

.chip-name {
  font-size: 0.9375rem;
  font-weight: 500;
  color: #171717;
}

/* ── Animations ── */
/* To make it truly infinite with any number of items:
   We animate -10% if we have 10 reps (1 rep distance).
*/
@keyframes marquee-left {
  0%   { transform: translateX(0); }
  100% { transform: translateX(calc(-10% - 2.4px)); } /* One rep + 1/10th of the track gap */
}
@keyframes marquee-right {
  0%   { transform: translateX(calc(-10% - 2.4px)); }
  100% { transform: translateX(0); }
}

/* ── Responsive ── */
@media (max-width: 639px) {
  .section-title { font-size: 1.75rem; }
  .marquee-fade::before,
  .marquee-fade::after { width: 40px; }
}
</style>