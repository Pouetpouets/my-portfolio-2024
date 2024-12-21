<script lang="ts">
  import AnimatedLogo from './AnimatedLogo.svelte';
</script>

<nav>
  <div class="nav-content">
    <div class="logo">
      <AnimatedLogo />
    </div>
    
    <div class="nav-links">
      <a href="#projects">Projects</a>
      <a href="#funfacts">Fun Facts</a>
      <button class="contact-btn">Contact</button>
    </div>
  </div>
</nav>

<style>
  nav {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    padding: 1rem 2rem;
    z-index: 100;
    background: #fafaf8;
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  }

  .nav-content {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .nav-links {
    display: flex;
    gap: 2rem;
    align-items: center;
  }

  @media (max-width: 768px) {
    .nav-content {
      flex-direction: column;
      gap: 1rem;
    }

    .nav-links {
      gap: 1rem;
    }
  }
</style>