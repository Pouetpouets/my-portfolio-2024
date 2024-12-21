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
          <stop offset="0%" stop-color="#049ef4" />
          <stop offset="100%" stop-color="#ff0066" />
        </linearGradient>
      </defs>
      <text x="50%" y="50%" text-anchor="middle" class="text-path">
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
    width: 240px;
    height: 40px;
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
    font-size: 24px;
    letter-spacing: 1px;
  }

  .animated-line {
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 100%;
    height: 2px;
    background: linear-gradient(
      to right,
      #049ef4,
      #ff0066
    );
    transform-origin: left center;
    animation: lineAnimation 2s infinite;
  }

  @keyframes lineAnimation {
    0% {
      transform: scaleX(0);
      opacity: 0;
    }
    50% {
      transform: scaleX(1);
      opacity: 1;
    }
    100% {
      transform: scaleX(0);
      opacity: 0;
      transform-origin: right center;
    }
  }
</style>