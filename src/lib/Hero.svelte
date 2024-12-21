<script lang="ts">
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';

  let visible = false;
  let currentText = '';
  let currentIcon = '';
  
  const textContent = [
    { text: "I'm a Frontend Developer", icon: '💻' },
    { text: "I love making burgers", icon: '🍔' },
    { text: "I enjoy hiking", icon: '🏃‍♂️' }
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
        <img src="/public/images/profile.jpg" alt="Lucas Legrand" class="profile-image">
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
            GitHub
          </a>
          <a href="https://twitter.com/lgrdlcs" target="_blank" rel="noopener noreferrer" class="social-link">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z"></path>
            </svg>
            Twitter
          </a>
          <a href="mailto:legrand.lucas0@gmail.com" class="social-link">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
              <polyline points="22,6 12,13 2,6"></polyline>
            </svg>
            Email
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
    background: #111;
    color: white;
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
    background: linear-gradient(135deg, #049ef4, #ff0066);
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
  }

  .cursor {
    animation: blink 1s infinite;
  }

  .image-container {
    flex: 0.8;
    height: 500px;
    border-radius: 16px;
    overflow: hidden;
  }

  .profile-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 16px;
    box-shadow: 0 0 20px rgba(4, 158, 244, 0.2);
  }

  .social-links {
    display: flex;
    gap: 1.5rem;
  }

  .social-link {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    color: white;
    text-decoration: none;
    padding: 0.75rem 1.25rem;
    border-radius: 8px;
    background: rgba(255, 255, 255, 0.1);
    transition: all 0.3s ease;
  }

  .social-link:hover {
    background: rgba(4, 158, 244, 0.2);
    transform: translateY(-2px);
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