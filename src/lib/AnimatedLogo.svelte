<script lang="ts">
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';
  
  let visible = false;
  
  onMount(() => {
    visible = true;
  });
</script>

{#if visible}
<div class="logo-container" in:fade={{ duration: 1000 }}>
  <div class="logo" aria-label="Lucas Legrand">
    <svg viewBox="0 0 400 50" class="logo-text">
      <defs>
        <linearGradient id="logoGradient" x1="0%" y1="0%" x2="100%" y2="0%">
          <stop offset="0%" stop-color="var(--light-sky-blue)" />
          <stop offset="50%" stop-color="var(--light-sky-blue)" />
          <stop offset="100%" stop-color="var(--carnation-pink)" />
        </linearGradient>
      </defs>
      <text x="50%" y="50%" text-anchor="middle" dominant-baseline="middle" class="text-path">
        Lucas Legrand
      </text>
    </svg>
    <div class="animated-line"></div>
  </div>
</div>
{/if}

<style>
  .logo-container {
    position: relative;
    padding: 0.5rem 1rem;
    cursor: pointer;
  }

  .logo {
    position: relative;
    width: 280px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .logo-text {
    width: 100%;
    height: 100%;
  }

  .text-path {
    fill: url(#logoGradient);
    font-family: 'LEMON MILK', sans-serif;
    font-size: 28px;
    letter-spacing: 2px;
    text-transform: uppercase;
  }

  .animated-line {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 2px;
    background: var(--gradient-primary);
    transform-origin: left center;
    animation: lineAnimation 2s infinite;
    background-size: 200% auto;
  }

  @keyframes lineAnimation {
    0% {
      transform: scaleX(0);
      opacity: 0;
      background-position: left center;
    }
    50% {
      transform: scaleX(1);
      opacity: 1;
      background-position: right center;
    }
    100% {
      transform: scaleX(0);
      opacity: 0;
      transform-origin: right center;
      background-position: left center;
    }
  }
</style>