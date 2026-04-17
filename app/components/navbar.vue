<template>
  <header class="navbar">
    <div class="container navbar-inner">
      <!-- Logo / Name -->
      <a href="/" class="navbar-brand font-display" @click.prevent="scrollToSection('home')">
        Adam Hariri
      </a>

      <!-- Desktop Nav Links -->
      <nav class="navbar-links" :class="{ open: menuOpen }">
        <a href="/" @click.prevent="scrollToSection('about')">About</a>
        <a href="/" @click.prevent="scrollToSection('projects')">Projects</a>
        <a href="/" @click.prevent="scrollToSection('skills')">Skills</a>
        <a href="/" @click.prevent="scrollToSection('contact')">Contact</a>
      </nav>

      <!-- CTA -->
      <div class="navbar-cta">
        <a href="/" class="btn-black" @click.prevent="scrollToSection('contact')">Hire me</a>
      </div>

      <!-- Hamburger -->
      <button class="hamburger" @click="toggleMenu" aria-label="Toggle menu">
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>
  </header>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
const menuOpen = ref(false)
const toggleMenu = () => { menuOpen.value = !menuOpen.value }
const closeMenu = () => { menuOpen.value = false }

const scrollToSection = (id: string) => {
  closeMenu()
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<style scoped>
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  background-color: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  border-bottom: 1px solid #e5e5e5;
}

.navbar-inner {
  display: flex;
  align-items: center;
  gap: 32px;
  height: 64px;
}

.navbar-brand {
  font-size: 1.1rem;
  font-weight: 500;
  color: #000000;
  text-decoration: none;
  white-space: nowrap;
  margin-right: auto;
  letter-spacing: -0.01em;
}

.navbar-links {
  display: flex;
  align-items: center;
  gap: 28px;
}

.navbar-links a {
  font-size: 1rem;
  font-weight: 400;
  color: #000000;
  text-decoration: none;
}

.navbar-links a:hover {
  color: #737373;
}

.navbar-cta {
  flex-shrink: 0;
}

.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}

.hamburger span {
  display: block;
  width: 22px;
  height: 1.5px;
  background-color: #000000;
}

@media (max-width: 639px) {
  .hamburger { display: flex; }
  .navbar-cta { display: none; }
  .navbar-links {
    display: none;
    position: absolute;
    top: 64px;
    left: 0;
    right: 0;
    flex-direction: column;
    align-items: stretch;
    gap: 0;
    background: #ffffff;
    border-bottom: 1px solid #e5e5e5;
    padding: 8px 0;
  }
  .navbar-links.open { display: flex; }
  .navbar-links a {
    padding: 12px 24px;
    border-bottom: 1px solid #fafafa;
  }
}
</style>
