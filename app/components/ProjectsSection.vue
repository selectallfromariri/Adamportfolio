<template>
  <section id="projects" class="section projects-section">
    <div class="container">
      <!-- Header -->
      <div class="projects-header">
        <div>
          <p class="section-label">Projects</p>
          <h2 class="font-display section-title">Things I've built.</h2>
        </div>
        <p class="projects-subtitle">
          A selection of projects I'm proud of.
        </p>
      </div>

      <!-- Featured Project (large card) -->
      <div class="project-featured card">
        <div class="featured-badge">Featured</div>
        <div class="featured-inner">
            <el-image
              src="/assets/images/Wedding Management.png"
              class="project-img-placeholder"
              fit="cover"
            />
          <div class="featured-content">
            <h3 class="project-title font-display">Wedding Management System</h3>
            <p class="project-desc">
              Wedding Management System where couples manage their wedding digitally and guests RSVP online, with an photo dump feature.
            </p>
            <div class="project-tags">
              <span class="skill-pill">Nuxt.js</span>
              <span class="skill-pill">Laravel</span>
              <span class="skill-pill">PostgreSQL</span>
            </div>
            <div class="project-links">
              <a href="https://github.com/selectallfromariri/Wedd" target="_blank" rel="noopener" class="btn-black">View on GitHub</a>
            </div>
          </div>
        </div>
      </div>

      <!-- Project grid -->
      <div class="projects-grid">
        <!-- Project Card 1 -->
        <div class="card project-card">
          <el-image
            src="/assets/images/TrackbackPTA.png"
            class="project-img-placeholder small"
            fit="cover"
          />
          <h3 class="project-title font-display">TrackBack : Web Based System</h3>
          <p class="project-desc">
            TrackBack is a web-based system that i did in my Diploma final year project, it designed to help individuals
            to find their lost items with the feature of reporting lost belongins to function for report found the item.
          </p>
          <div class="project-tags">
            <span class="skill-pill">PHP</span>
            <span class="skill-pill">Javascript</span>
            <span class="skill-pill">MySQL</span>
            <span class="skill-pill">OpenStreetAPI</span>
            <span class="skill-pill">PHPMailer</span>
          </div>
        </div>

        <!-- Project Card 2 -->
        <div class="card project-card">
          <el-image
            src="/assets/images/pokedex.jpeg"
            class="project-img-placeholder small"
            fit="cover"
          />
          <h3 class="project-title font-display">Pokedex</h3>
          <p class="project-s">
            A Pokedex application that allows users to search for Pokemon and view their information, build it because i want to learn react native.
          </p>
          <div class="project-t">
            <span class="skill-pill">React Native</span>
            <span class="skill-pill">pokeApi</span>
          </div>
            <div class="project-l">
              <a href="https://github.com/selectallfromariri/Pokedex" target="_blank" rel="noopener" class="btn-black">View on GitHub</a>
            </div>
            
        </div>
      </div>

      <!-- More coming soon -->
      <p class="more-soon">· · · more coming soon</p>
    </div>
    
  </section>
</template>

<style scoped>
.projects-section {
  background-color: #ffffff;
  border-top: 1px solid #e5e5e5;
}

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
  color: #000000;
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

/* Featured */
.project-featured {
  margin-bottom: 32px;
  position: relative;
}

.featured-badge {
  display: inline-block;
  font-size: 0.75rem;
  font-weight: 500;
  color: #262626;
  background: #e5e5e5;
  border-radius: 9999px;
  padding: 3px 12px;
  margin-bottom: 20px;
  text-transform: uppercase;
  letter-spacing: 0.06em;
}

.featured-inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  align-items: start;
}

/* Grid */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

/* Card internals */
.project-card {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.project-img-placeholder {
  width: 100%;
  aspect-ratio: 16 / 9;
  border-radius: 8px;
  background: #fafafa;
  border: 1px solid #e5e5e5;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 8px;
  color: #a3a3a3;
  font-size: 0.75rem;
  font-weight: 400;
}

.project-img-placeholder.small {
  aspect-ratio: 16 / 7;
}

.project-title {
  font-size: 1.25rem;
  font-weight: 500;
  color: #000000;
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

.project-s {
  font-size: 0.9375rem;
  color: #737373;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.project-links {
  display: flex;
  gap: 10px;
  margin-top: 20px;
  flex-wrap: wrap;
  padding-top: 4px;
}

.project-l{
  display: flex;
  gap: 10px;
  margin-top: 85px;
  flex-wrap: wrap;
  padding-top: 4px;
}

@media (max-width: 767px) {
  .featured-inner { grid-template-columns: 1fr; gap: 24px; }
  .projects-grid { grid-template-columns: 1fr; }
  .section-title { font-size: 1.75rem; }
  .projects-subtitle { max-width: 100%; }
}

.more-soon {
  text-align: center;
  font-size: 0.875rem;
  color: #a3a3a3;
  margin: 32px 0 0;
  letter-spacing: 0.08em;
}
</style>
