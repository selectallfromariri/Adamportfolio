<template>
  <section id="contact" class="section contact-section">
    <div class="container">
      <div class="contact-grid">
        <!-- Left: heading + info -->
        <div class="contact-info">
          <p class="section-label">Contact</p>
          <h2 class="font-display section-title">Let's work together.</h2>
          <p class="contact-body">
            Whether you have a project in mind, a question, or just want to say hi, my inbox is always open.
          </p>

          <div class="contact-links">
            <a href="mailto:haririiadam040@gmail.com" class="contact-link-item">
              <span class="contact-link-icon">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                  <polyline points="22,6 12,13 2,6"/>
                </svg>
              </span>
              <span>haririiadam040@gmail.com</span>
            </a>
            <a href="https://www.linkedin.com/in/adam-hariri-ab82652a6/" target="_blank" rel="noopener" class="contact-link-item">
              <span class="contact-link-icon">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                </svg>
              </span>
              <span>linkedin.com/in/adamhariri</span>
            </a>
            <a href="https://github.com/selectallfromariri" target="_blank" rel="noopener" class="contact-link-item">
              <span class="contact-link-icon">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/>
                </svg>
              </span>
              <span>github.com/selectallfromariri</span>
            </a>
          </div>
        </div>

        <!-- Right: contact form -->
        <div class="contact-form-wrap">
          <form class="contact-form card" @submit.prevent="handleSubmit">
            <div class="form-group">
              <label for="contact-name" class="form-label">Name</label>
              <input
                id="contact-name"
                v-model="form.name"
                type="text"
                class="form-input"
                placeholder="Your name"
                required
              />
            </div>

            <div class="form-group">
              <label for="contact-email" class="form-label">Email</label>
              <input
                id="contact-email"
                v-model="form.email"
                type="email"
                class="form-input"
                placeholder="you@example.com"
                required
              />
            </div>

            <div class="form-group">
              <label for="contact-subject" class="form-label">Subject</label>
              <input
                id="contact-subject"
                v-model="form.subject"
                type="text"
                class="form-input"
                placeholder="What's this about?"
              />
            </div>

            <div class="form-group">
              <label for="contact-message" class="form-label">Message</label>
              <textarea
                id="contact-message"
                v-model="form.message"
                class="form-textarea"
                rows="5"
                placeholder="Tell me about your project or idea..."
                required
              ></textarea>
            </div>

            <button type="submit" class="btn-black" style="width: 100%; justify-content: center;">
              Send Message
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts" setup>
import { reactive } from 'vue'

const form = reactive({ name: '', email: '', subject: '', message: '' })

const handleSubmit = () => {
  // Wire up your preferred contact service here (Formspree, EmailJS, etc.)
  const mailto = `mailto:you@example.com?subject=${encodeURIComponent(form.subject || 'Portfolio Contact')}&body=${encodeURIComponent(`From: ${form.name} (${form.email})\n\n${form.message}`)}`
  window.location.href = mailto
}
</script>

<style scoped>
.contact-section {
  background-color: #ffffff;
  border-top: 1px solid #e5e5e5;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1.3fr;
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
  margin: 0 0 20px;
  letter-spacing: -0.02em;
}

.contact-body {
  font-size: 1rem;
  color: #737373;
  line-height: 1.65;
  margin: 0 0 32px;
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.contact-link-item {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 0.9375rem;
  color: #262626;
  text-decoration: none;
}
.contact-link-item:hover { color: #737373; }

.contact-link-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 9999px;
  border: 1px solid #e5e5e5;
  color: #000000;
  flex-shrink: 0;
}

/* Form */
.contact-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-label {
  font-size: 0.8125rem;
  font-weight: 500;
  color: #262626;
  text-transform: uppercase;
  letter-spacing: 0.06em;
}

.form-input,
.form-textarea {
  background: #ffffff;
  border: 1px solid #e5e5e5;
  border-radius: 9999px;
  padding: 10px 18px;
  font-size: 0.9375rem;
  font-family: inherit;
  color: #000000;
  outline: none;
  width: 100%;
}

.form-textarea {
  border-radius: 12px;
  resize: vertical;
  min-height: 120px;
  line-height: 1.6;
}

.form-input:focus,
.form-textarea:focus {
  border-color: #737373;
}

.form-input::placeholder,
.form-textarea::placeholder {
  color: #a3a3a3;
}

@media (max-width: 767px) {
  .contact-grid { grid-template-columns: 1fr; gap: 40px; }
  .section-title { font-size: 1.75rem; }
}
</style>
