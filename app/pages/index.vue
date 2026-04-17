<template>
  <div>
    <Navbar />
    <main>
      <HeroSection />
      <hr class="divider" />
      <AboutSection />
      <hr class="divider" />
      <ProjectsSection />
      <hr class="divider" />
      <SkillsSection />
      <hr class="divider" />
      <ContactSection />
    </main>
    <FooterSection />
  </div>
</template>

<script lang="ts" setup>
useHead({
  title: 'Your Name — Portfolio',
  meta: [
    { name: 'description', content: 'Full-Stack Developer & Designer. Building clean, thoughtful digital products.' },
    { property: 'og:title', content: 'Your Name — Portfolio' },
    { property: 'og:description', content: 'Full-Stack Developer & Designer. Building clean, thoughtful digital products.' },
  ],
  link: [
    { rel: 'preconnect', href: 'https://fonts.googleapis.com' },
  ],
})
</script>