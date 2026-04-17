<template>
  <section id="about" class="section about-section">
    <div class="container">
      <div class="about-grid">
        <!-- Left: heading -->
        <div class="about-heading-col">
          <p class="section-label">About me</p>
          <h2 class="font-display section-title">A little bit about who I am.</h2>
        </div>

        <!-- Right: content -->
        <div class="about-content-col">
          <p class="about-body">
            I’m a student who enjoys building scalable system. 
            Currently studying in University Malaysia Pahang Al-Sultan Abdullah in the field of Software Engineering,
            and I’m passionate about writing clean,
            maintainable code while creating seamless user experiences.
          </p>
          <p class="about-body">
            I’m based in Malaysia and work with both frontend and backend technologies <bold>(*ps more to backend)</bold>. I’m always eager to learn new tools and improve my skills.
          </p>

          <!-- Quick facts -->
          <div class="about-facts">
            <div class="fact-item">
              <span class="fact-label">Location</span>
              <span class="fact-value">Malaysia</span>
            </div>
            <div class="fact-item">
              <span class="fact-label">Experience</span>
              <span class="fact-value">Internship</span>
            </div>
            <div class="fact-item">
              <span class="fact-label">Availability</span>
              <span class="fact-value">Open to opportunities</span>
            </div>
            <div class="fact-item">
              <span class="fact-label">Languages</span>
              <span class="fact-value">English, Malay</span>
            </div>
          </div>

          <!-- Resume download -->
          <!-- <a href="/resume.pdf" target="_blank" class="btn-gray" style="width: fit-content; margin-top: 4px;">
            Download Resume
          </a> -->
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-section {
  background-color: #fafafa;
  border-top: 1px solid #e5e5e5;
  border-bottom: 1px solid #e5e5e5;
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 64px;
  align-items: start;
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
  margin: 0;
  letter-spacing: -0.02em;
}

.about-content-col {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.about-body {
  font-size: 1rem;
  color: #525252;
  line-height: 1.65;
  margin: 0;
}

.about-facts {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  padding-top: 4px;
}

.fact-item {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.fact-label {
  font-size: 0.75rem;
  font-weight: 400;
  color: #a3a3a3;
  text-transform: uppercase;
  letter-spacing: 0.06em;
}

.fact-value {
  font-size: 0.9375rem;
  font-weight: 400;
  color: #262626;
}

@media (max-width: 767px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: 32px;
  }
  .section-title { font-size: 1.75rem; }
  .about-facts { grid-template-columns: 1fr; }
}
</style>
