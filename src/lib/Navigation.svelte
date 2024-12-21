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
      <a href="#contact" class="contact-btn">Contact</a>
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
    background: rgba(17, 17, 17, 0.8);
    backdrop-filter: blur(10px);
    border-bottom: 1px solid rgba(205, 180, 219, 0.1);
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

  a {
    color: var(--text-primary);
    text-decoration: none;
    font-size: 1rem;
    transition: all 0.3s ease;
    padding: 0.5rem 1rem;
    border-radius: 8px;
    position: relative;
  }

  a::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 2px;
    background: var(--gradient-primary);
    transform: scaleX(0);
    transform-origin: right;
    transition: transform 0.3s ease;
  }

  a:hover::after {
    transform: scaleX(1);
    transform-origin: left;
  }

  .contact-btn {
    background: var(--gradient-primary);
    color: var(--text-primary);
    border: none;
    padding: 0.5rem 1.5rem;
    border-radius: 8px;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.3s ease;
    background-size: 200% auto;
  }

  .contact-btn:hover {
    background-position: right center;
    transform: translateY(-2px);
  }

  .contact-btn::after {
    display: none;
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