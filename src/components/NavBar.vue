<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  document.body.classList.add('dark-mode')
})
</script>

<template>
  <nav class="navbar">
    <!-- TITLE -->
    <div class="nav-title">
      automata-theory project
    </div>


  </nav>
</template>

<style scoped>
/* NAVBAR CONTAINER */
.navbar {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding: 14px 24px;
  background: #0d1117;
  border-bottom: 1px solid #30363d;
  transition: all 0.3s ease;
}

/* TITLE */
.nav-title {
  font-size: 16px;
  font-weight: 600;
  color: #e6edf3;
  transition: color 0.3s;
  letter-spacing: 0.5px;
}

@media (max-width: 640px) {
  .navbar {
    padding: 12px 16px;
  }
  
  .nav-title {
    font-size: 14px;
  }
}
</style>