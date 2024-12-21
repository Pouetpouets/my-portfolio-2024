<script lang="ts">
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  import ThreeScene from './ThreeScene.svelte';

  let visible = false;
  onMount(() => {
    visible = true;
  });
</script>

<section id="contact">
  {#if visible}
    <div class="content" in:fade={{duration: 1000}}>
      <h2 in:fly={{y: 50, duration: 1000}}>Get in Touch</h2>
      <div class="contact-container">
        <div class="three-container">
          <ThreeScene />
        </div>
        <a href="mailto:legrand.lucas0@gmail.com" class="contact-link" in:fly={{y: 20, duration: 1000, delay: 300}}>
          <svg xmlns="http://www.w3.org/2000/svg" class="icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
            <polyline points="22,6 12,13 2,6"/>
          </svg>
          legrand.lucas0@gmail.com
        </a>
      </div>
    </div>
  {/if}
</section>

<style>
  section {
    min-height: 50vh;
    padding: 4rem 2rem;
    background: #111;
    color: white;
  }

  .content {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
  }

  h2 {
    font-size: 2.5rem;
    margin-bottom: 2rem;
    text-align: center;
    background: linear-gradient(135deg, var(--light-sky-blue), var(--uranian-blue));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .contact-container {
    width: 100%;
    max-width: 400px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
    padding: 2rem;
    background: rgba(255, 255, 255, 0.05);
    border-radius: 16px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
  }

  .three-container {
    width: 100%;
    height: 300px;
    border-radius: 12px;
    overflow: hidden;
    background: rgba(0, 0, 0, 0.3);
  }

  .contact-link {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    color: var(  --light-sky-blue);
    text-decoration: none;
    font-size: 1.1rem;
    padding: 1rem 1.5rem;
    border: 2px solid var(  --light-sky-blue);
    border-radius: 8px;
    transition: all 0.3s ease;
  }

  .contact-link:hover {
    color: #ff0066;
    border-color: #ff0066;
    transform: translateY(-2px);
  }

  .icon {
    width: 24px;
    height: 24px;
  }

  @media (max-width: 768px) {
    .contact-container {
      padding: 1rem;
    }

    .three-container {
      height: 250px;
    }
  }
</style>