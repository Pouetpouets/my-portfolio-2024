<script lang="ts">
  import ThreeScene from './lib/ThreeScene.svelte';
  import Navigation from './lib/Navigation.svelte';
  import Projects from './lib/Projects.svelte';
  import FunFacts from './lib/FunFacts.svelte';
</script>

<main>
  <Navigation />
  <ThreeScene />
  <Projects />
  <FunFacts />
</main>

<style>
  main {
    width: 100vw;
    overflow-x: hidden;
    background: #000;
  }
</style>