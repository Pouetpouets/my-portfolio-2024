<script lang="ts">
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';

  let visible = false;
  let currentText = '';
  let currentIcon = '';
  
  const textContent = [
    { text: "I'm a Frontend Developer", icon: '💻' },
    { text: "I love making burgers", icon: '🍔' },
    { text: "I enjoy trails", icon: '🏃‍♂️' }
  ];
  
  let currentIndex = 0;
  let charIndex = 0;
  
  onMount(() => {
    visible = true;
    typeText();
  });

  function typeText() {
    currentIcon = textContent[currentIndex].icon;
    if (charIndex < textContent[currentIndex].text.length) {
      currentText += textContent[currentIndex].text[charIndex];
      charIndex++;
      setTimeout(typeText, 100);
    } else {
      setTimeout(() => {
        deleteText();
      }, 2000);
    }
  }

  function deleteText() {
    if (currentText.length > 0) {
      currentText = currentText.slice(0, -1);
      setTimeout(deleteText, 50);
    } else {
      currentIndex = (currentIndex + 1) % textContent.length;
      charIndex = 0;
      setTimeout(typeText, 500);
    }
  }
</script>

<section class="hero">
  {#if visible}
    <div class="hero-content" in:fade={{ duration: 1000 }}>
      <div class="image-container" in:fly={{ x: -50, duration: 1000 }}>
        <img src="/images/profile.jpg" alt="Lucas Legrand" class="profile-image">
      </div>
      
      <div class="text-content">
        <h1 in:fly={{ y: 50, duration: 1000 }}>Lucas Legrand</h1>
        <div class="typed-container">
          <span class="icon">{currentIcon}</span>
          <div class="typed-text">{currentText}<span class="cursor">|</span></div>
        </div>
        
        <div class="social-links" in:fly={{ y: 20, duration: 1000, delay: 500 }}>
          <a href="https://github.com/Pouetpouets" target="_blank" rel="noopener noreferrer" class="social-link">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path>
            </svg>
          </a>
          <a href="https://twitter.com/lgrdlcs" target="_blank" rel="noopener noreferrer" class="social-link">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z"></path>
            </svg>
          </a>
          <a href="mailto:legrand.lucas0@gmail.com" class="social-link">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
              <polyline points="22,6 12,13 2,6"></polyline>
            </svg>
          </a>
        </div>
      </div>
    </div>
  {/if}
</section>

<style>
  .hero {
    min-height: 100vh;
    padding: 6rem 2rem 2rem;
    background: var(--bg-primary);
    color: var(--text-primary);
    display: flex;
    align-items: center;
  }

  .hero-content {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    gap: 4rem;
  }

  .text-content {
    flex: 1;
  }

  h1 {
    font-size: 3.5rem;
    margin-bottom: 2rem;
    width: 30rem;
    background: var(--light-sky-blue);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .typed-container {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 3rem;
  }

  .icon {
    font-size: 2.5rem;
    min-width: 3rem;
  }

  .typed-text {
    font-size: 2rem;
    min-height: 3rem;
    color: var(--uranian-blue);
  }

  .cursor {
    animation: blink 1s infinite;
    color: var(--light-sky-blue);
  }

  .image-container {
    flex: 0.8;
    height: 300px;
    border-radius: 50px;
    overflow: hidden;
    position: relative;
  }

  /* .image-container::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    border-radius: 16px;
    background: var(--gradient-full);
    opacity: 0;
    transition: opacity 0.3s ease;
  } */

  .image-container:hover::after {
    opacity: 0.2;
  }

  .profile-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 16px;
    box-shadow: 0 0 20px rgba(205, 180, 219, 0.2);
    transition: all 0.3s ease;
  }

  .profile-image:hover {
    animation: pulse 2s infinite ease-in-out;
  }

  @keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.03); }
    100% { transform: scale(1); }
  }

  .social-links {
    display: flex;
    gap: 1.5rem;
  }

  .social-link {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    color: var(--text-primary);
    text-decoration: none;
    padding: 0.75rem 1.25rem;
    border-radius: 8px;
    background: var(--bg-secondary);
    transition: all 0.3s ease;
    border: 1px solid transparent;
  }

  .social-link:hover {
    background: rgba(205, 180, 219, 0.1);
    transform: translateY(-2px);
    border-color: var(--light-sky-blue);
    color: var(--light-sky-blue);
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  @media (max-width: 968px) {
    .hero-content {
      flex-direction: column;
      text-align: center;
      gap: 2rem;
    }

    .image-container {
      width: 300px;
      height: 300px;
    }

    .typed-container {
      justify-content: center;
    }

    .social-links {
      justify-content: center;
      flex-wrap: wrap;
    }

    h1 {
      font-size: 2.5rem;
    }

    .typed-text {
      font-size: 1.5rem;
    }
  }
</style>