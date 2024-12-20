<script lang="ts">
  import ThreeScene from './lib/ThreeScene.svelte';
  import Navigation from './lib/Navigation.svelte';
</script>

<main>
  <Navigation />
  <ThreeScene />
</main>

<style>
  main {
    width: 100vw;
    height: 100vh;
    margin: 0;
    padding: 0;
    overflow: hidden;
    background: #000;
  }
</style>