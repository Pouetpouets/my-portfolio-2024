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
      <h2 in:fly={{y: 50, duration: 1000}}>Contact</h2>
      <div class="contact-container">
        <div class="contact-info">
          <a href="mailto:legrand.lucas0@gmail.com" class="email-link">
            legrand.lucas0@gmail.com
          </a>
        </div>
        <div class="scene-container">
          <ThreeScene />
        </div>
      </div>
    </div>
  {/if}
</section>

<style>
  section {
    min-height: 100vh;
    padding: 6rem 2rem 2rem;
    background: #111;
    color: white;
  }

  .content {
    max-width: 1200px;
    margin: 0 auto;
  }

  h2 {
    font-size: 2.5rem;
    margin-bottom: 3rem;
    text-align: center;
  }

  .contact-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
  }

  .contact-info {
    text-align: center;
  }

  .email-link {
    color: #049ef4;
    text-decoration: none;
    font-size: 1.5rem;
    transition: color 0.3s ease;
    display: inline-block;
    padding: 1rem 2rem;
    border: 2px solid #049ef4;
    border-radius: 8px;
  }

  .email-link:hover {
    color: #ff0066;
    border-color: #ff0066;
  }

  .scene-container {
    width: 100%;
    max-width: 600px;
    height: 400px;
    border-radius: 12px;
    overflow: hidden;
    background: rgba(255, 255, 255, 0.05);
  }
</style>