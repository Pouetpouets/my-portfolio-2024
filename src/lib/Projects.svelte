<script lang="ts">
  import { fade, fly } from 'svelte/transition';
  import { onMount } from 'svelte';

  let visible = false;
  let repositories = [];
  
  onMount(async () => {
    visible = true;
    try {
      const response = await fetch('https://api.github.com/users/Pouetpouets/repos?sort=updated&per_page=3');
      repositories = await response.json();
    } catch (error) {
      console.error('Error fetching repositories:', error);
    }
  });

  function formatDate(dateString: string) {
    const date = new Date(dateString);
    return new Intl.DateTimeFormat('en-US', {
      year: 'numeric',
      month: 'short',
      day: 'numeric'
    }).format(date);
  }
</script>

<section id="projects">
  {#if visible}
    <div class="content" in:fade={{duration: 1000}}>
      <h2 in:fly={{y: 50, duration: 1000}}>Latest Projects & Contributions</h2>
      
      <div class="github-stats">
        <!-- GitHub Stats Card -->
        <div class="stats-wrapper" in:fly={{y: 50, duration: 1000, delay: 200}}>
          <a href="https://github.com/Pouetpouets" target="_blank" rel="noopener noreferrer" class="github-profile">
            <img 
              src="https://github-readme-stats.vercel.app/api?username=Pouetpouets&show_icons=true&theme=tokyonight&hide_border=true&count_private=true"
              alt="GitHub Stats"
              class="stats-card"
            />
          </a>
        </div>

        <!-- Languages Card -->
        <div class="stats-wrapper" in:fly={{y: 50, duration: 1000, delay: 400}}>
          <img 
            src="https://github-readme-stats.vercel.app/api/top-langs/?username=Pouetpouets&layout=compact&theme=tokyonight&hide_border=true"
            alt="Top Languages"
            class="stats-card"
          />
        </div>
      </div>

      <!-- Contribution Graph -->
      <div class="contributions" in:fly={{y: 50, duration: 1000, delay: 600}}>
        <img 
          src="https://github-readme-activity-graph.vercel.app/graph?username=Pouetpouets&theme=react-dark&hide_border=true"
          alt="Contribution Graph"
          class="contribution-graph"
        />
      </div>

      <h3 class="recent-title" in:fly={{y: 50, duration: 1000}}>Recent Projects</h3>
      <div class="projects-grid">
        {#each repositories as repo}
          <div 
            class="project-card"
            in:fly={{y: 50, duration: 1000}}
          >
            <div class="project-info">
              <h4>
                <a href={repo.html_url} target="_blank" rel="noopener noreferrer">
                  {repo.name}
                </a>
              </h4>
              <p>{repo.description || 'No description available'}</p>
              <div class="repo-meta">
                <span class="language" style="color: {repo.language === 'JavaScript' ? '#f1e05a' : 
                                                    repo.language === 'TypeScript' ? '#2b7489' : 
                                                    repo.language === 'Ruby' ? '#701516' : '#049ef4'}">
                  ● {repo.language || 'Unknown'}
                </span>
                <span class="date">Updated: {formatDate(repo.updated_at)}</span>
              </div>
              <div class="tags">
                {#if repo.topics && repo.topics.length}
                  {#each repo.topics as topic}
                    <span class="tag">{topic}</span>
                  {/each}
                {/if}
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

  .recent-title {
    font-size: 2rem;
    margin: 3rem 0;
    text-align: center;
    color: #049ef4;
  }

  .github-stats {
    display: flex;
    justify-content: center;
    gap: 2rem;
    margin-bottom: 3rem;
    flex-wrap: wrap;
  }

  .stats-wrapper {
    flex: 1;
    min-width: 300px;
    max-width: 500px;
  }

  .stats-card {
    width: 100%;
    height: auto;
    border-radius: 10px;
    transition: transform 0.3s ease;
  }

  .stats-card:hover {
    transform: translateY(-5px);
  }

  .contributions {
    margin: 3rem 0;
    width: 100%;
    overflow: hidden;
    border-radius: 10px;
  }

  .contribution-graph {
    width: 100%;
    height: auto;
    min-height: 200px;
    transition: transform 0.3s ease;
  }

  .contribution-graph:hover {
    transform: translateY(-5px);
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
    height: 100%;
  }

  .project-card:hover {
    transform: translateY(-5px);
  }

  .project-info {
    padding: 1.5rem;
  }

  h4 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
  }

  h4 a {
    color: #049ef4;
    text-decoration: none;
    transition: color 0.3s ease;
  }

  h4 a:hover {
    color: #ff0066;
  }

  p {
    color: #ccc;
    margin-bottom: 1rem;
    line-height: 1.6;
  }

  .repo-meta {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
    font-size: 0.875rem;
    color: #888;
  }

  .tags {
    display: flex;
    gap: 0.5rem;
    flex-wrap: wrap;
  }

  .tag {
    background: rgba(4, 158, 244, 0.2);
    color: #049ef4;
    padding: 0.25rem 0.75rem;
    border-radius: 999px;
    font-size: 0.875rem;
  }

  @media (max-width: 768px) {
    .projects-grid {
      grid-template-columns: 1fr;
    }

    .github-stats {
      flex-direction: column;
      align-items: center;
    }

    .stats-wrapper {
      width: 100%;
    }
  }
</style>