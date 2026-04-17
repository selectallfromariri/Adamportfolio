<template>
  <footer class="footer">
    <div class="container footer-inner">
      <p class="footer-copy">
        &copy; 2026 All rights reserved. Crafted with passion.
      </p>
    </div>
  </footer>
</template>

<script lang="ts" setup>
</script>

<style scoped>
.footer {
  background-color: #090909;
  color: #737373;
  padding: 32px 0;
}

.footer-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 16px;
}

.footer-name {
  font-size: 1rem;
  font-weight: 500;
  color: #ffffff;
}

.footer-copy {
  font-size: 0.875rem;
  color: #737373;
  margin: 0;
}

.footer-links {
  display: flex;
  gap: 20px;
}

.footer-links a {
  font-size: 0.875rem;
  color: #737373;
  text-decoration: none;
}

.footer-links a:hover {
  color: #ffffff;
}

@media (max-width: 639px) {
  .footer-inner { flex-direction: column; align-items: flex-start; gap: 12px; }
}
</style>
