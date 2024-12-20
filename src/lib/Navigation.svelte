<script lang="ts">
  const name = "Lucas"; // You can change this to your full name
</script>

<nav>
  <div class="nav-content">
    <div class="logo">
      {name}
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
    padding: 1.5rem 2rem;
    z-index: 100;
    background: rgba(0, 0, 0, 0.8);
    backdrop-filter: blur(10px);
  }

  .nav-content {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .logo {
    font-size: 1.5rem;
    font-weight: bold;
    color: white;
    text-transform: uppercase;
    letter-spacing: 2px;
  }

  .nav-links {
    display: flex;
    gap: 2rem;
    align-items: center;
  }

  a {
    color: white;
    text-decoration: none;
    font-size: 1rem;
    transition: color 0.3s ease;
  }

  a:hover {
    color: #049ef4;
  }

  .contact-btn {
    background: #049ef4;
    color: white;
    border: none;
    padding: 0.5rem 1.5rem;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .contact-btn:hover {
    background: #0384d0;
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