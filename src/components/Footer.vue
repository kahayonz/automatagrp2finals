<template>
  <footer class="bottom-navbar">
    <div class="footer-content">
      <div class="course-info">
        AUTOMATA THEORY AND FORMAL LANGUAGES <strong>DLSUD</strong>
      </div>
      <div class="team-info">
        led and developed by 
        <span>Marc Daniel Cajayon</span>, 
        <span>Gabriel Castillo</span>, 
        <span>Luis Miguel Trias</span>, 
        <span>Gian Paolo Ybut</span>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.bottom-navbar {
  width: 100%;
  background: #0d1117;
  color: #8b949e;
  padding: 16px 24px;
  border-top: 1px solid #30363d;
  margin-top: 40px;
  font-family: monospace;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
}

.course-info {
  font-size: 13px;
  letter-spacing: 0.05em;
  font-weight: 500;
  text-transform: uppercase;
}

.course-info strong {
  color: #3fb950;
  margin-left: 4px;
  font-weight: 600;
}

.team-info {
  font-size: 12px;
  color: #8b949e;
  text-align: right;
  line-height: 1.4;
}

.team-info span {
  color: #e6edf3;
  font-weight: 500;
}

@media (max-width: 850px) {
  .footer-content {
    flex-direction: column;
    text-align: center;
    gap: 12px;
  }
  
  .team-info {
    text-align: center;
    word-break: break-word;
    overflow-wrap: break-word;
    max-width: 100%;
  }

  .bottom-navbar {
    padding: 24px 16px;
    box-sizing: border-box;
  }
}
</style>
