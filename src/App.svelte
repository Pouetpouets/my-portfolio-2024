<script lang="ts">
  import ThreeScene from './lib/ThreeScene.svelte';
  import Navigation from './lib/Navigation.svelte';
  import Projects from './lib/Projects.svelte';
  import FunFacts from './lib/FunFacts.svelte';
</script>

<main>
  <Navigation />
  <div class="scene-wrapper">
    <ThreeScene />
  </div>
  <Projects />
  <FunFacts />
</main>

<style>
  main {
    width: 100vw;
    background: #000;
  }

  .scene-wrapper {
    height: 100vh;
    overflow: hidden;
  }
</style>