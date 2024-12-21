<script lang="ts">
  import Navigation from './lib/Navigation.svelte';
  import Hero from './lib/Hero.svelte';
  import Projects from './lib/Projects.svelte';
  import FunFacts from './lib/FunFacts.svelte';
  import Contact from './lib/Contact.svelte';
</script>

<main>
  <Navigation />
  <Hero />
  <Projects />
  <FunFacts />
  <Contact />
</main>

<style>
  main {
    width: 100vw;
    background: #000;
  }
</style>