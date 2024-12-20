<script lang="ts">
  import { fade, fly } from 'svelte/transition';
  import { onMount } from 'svelte';

  const projects = [
    {
      title: "Project 1",
      description: "Description of project 1. This is a brief overview of what the project does and what technologies were used.",
      tags: ["React", "Node.js", "MongoDB"],
      image: "/api/placeholder/400/300"
    },
    {
      title: "Project 2",
      description: "Description of project 2. Highlighting the key features and challenges overcome during development.",
      tags: ["Svelte", "Three.js", "TypeScript"],
      image: "/api/placeholder/400/300"
    },
    {
      title: "Project 3",
      description: "Description of project 3. Showcasing the problem solved and the impact of the solution.",
      tags: ["Vue", "Express", "PostgreSQL"],
      image: "/api/placeholder/400/300"
    }
  ];

  let visible = false;
  
  onMount(() => {
    visible = true;
  });
</script>

<section id="projects">
  {#if visible}
    <div class="content" in:fade={{duration: 1000}}>
      <h2 in:fly={{y: 50, duration: 1000}}>Projects</h2>
      <div class="projects-grid">
        {#each projects as project, i}
          <div 
            class="project-card"
            in:fly={{y: 50, duration: 1000, delay: 200 * i}}
          >
            <img src={project.image} alt={project.title} />
            <div class="project-info">
              <h3>{project.title}</h3>
              <p>{project.description}</p>
              <div class="tags">
                {#each project.tags as tag}
                  <span class="tag">{tag}</span>
                {/each}
              </div>
            </div>
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

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }

  .project-card {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.3s ease;
  }

  .project-card:hover {
    transform: translateY(-5px);
  }

  img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }

  .project-info {
    padding: 1.5rem;
  }

  h3 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
  }

  p {
    color: #ccc;
    margin-bottom: 1rem;
    line-height: 1.6;
  }

  .tags {
    display: flex;
    gap: 0.5rem;
    flex-wrap: wrap;
  }

  .tag {
    background: #049ef4;
    color: white;
    padding: 0.25rem 0.75rem;
    border-radius: 999px;
    font-size: 0.875rem;
  }
</style>