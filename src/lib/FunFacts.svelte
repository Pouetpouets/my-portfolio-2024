<script lang="ts">
  import { fade, fly, scale } from 'svelte/transition.js';
  import { onMount } from 'svelte';

  const facts = [
    {
      icon: "🌎",
      title: "Traveler",
      description: "Visited 20+ countries across 4 continents"
    },
    {
      icon: "🎸",
      title: "Musician",
      description: "Play guitar and piano in my free time"
    },
    {
      icon: "🏃‍♂️",
      title: "Runner",
      description: "Completed 3 marathons and counting"
    },
    {
      icon: "📚",
      title: "Bookworm",
      description: "Read 30 books per year on average"
    }
  ];

  let visible = false;
  
  onMount(() => {
    visible = true;
  });
</script>

<section id="funfacts">
  {#if visible}
    <div class="content" in:fade={{duration: 1000}}>
      <h2 in:fly={{y: 50, duration: 1000}}>Fun Facts</h2>
      <div class="facts-grid">
        {#each facts as fact, i}
          <div 
            class="fact-card"
            in:scale={{
              duration: 800,
              delay: 200 * i,
              start: 0.5
            }}
          >
            <div class="icon">{fact.icon}</div>
            <h3>{fact.title}</h3>
            <p>{fact.description}</p>
          </div>
        {/each}
      </div>
    </div>
  {/if}
</section>

<style>
  section {
    min-height: 100vh;
    padding: 6rem 2rem 2rem;
    background: #000;
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

  .facts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    padding: 2rem;
  }

  .fact-card {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 12px;
    padding: 2rem;
    text-align: center;
    transition: transform 0.3s ease;
  }

  .fact-card:hover {
    transform: translateY(-5px);
  }

  .icon {
    font-size: 3rem;
    margin-bottom: 1rem;
  }

  h3 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    color: #049ef4;
  }

  p {
    color: #ccc;
    line-height: 1.6;
  }
</style>