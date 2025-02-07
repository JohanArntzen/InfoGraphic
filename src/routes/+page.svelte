<script>
  import { onMount } from 'svelte';
  import { theme } from '$lib/stores/theme';

  let images = [
    { src: '/images/image1.jpg', text: 'Image 1 description' },
    { src: '/images/image2.jpg', text: 'Image 2 description' },
    { src: '/images/image3.jpg', text: 'Image 3 description' }
  ];

  function toggleTheme() {
    theme.update(t => t === 'light' ? 'dark' : 'light');
  }
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600&family=Plus+Jakarta+Sans:wght@400;500;600&display=swap" rel="stylesheet">
</svelte:head>

<nav>
  <div class="nav-content">
    <h1>Infographic</h1>
    <button class="theme-toggle" on:click={toggleTheme}>
      {#if $theme === 'light'}
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="12" cy="12" r="5"/>
          <line x1="12" y1="1" x2="12" y2="3"/>
          <line x1="12" y1="21" x2="12" y2="23"/>
          <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/>
          <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/>
          <line x1="1" y1="12" x2="3" y2="12"/>
          <line x1="21" y1="12" x2="23" y2="12"/>
          <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/>
          <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/>
        </svg>
      {:else}
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>
        </svg>
      {/if}
    </button>
  </div>
</nav>

<div class="container">
  {#each images as { src, text }}
    <div class="item">
      <div class="filler-box">
        <img {src} alt={text} />
        <div class="placeholder">
          <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <rect x="3" y="3" width="18" height="18" rx="2" ry="2"/>
            <circle cx="8.5" cy="8.5" r="1.5"/>
            <polyline points="21 15 16 10 5 21"/>
          </svg>
        </div>
      </div>
      <div class="text-box">
        <p>{text}</p>
      </div>
    </div>
  {/each}
</div>

<style>
  :global([data-theme="dark"]) {
    --bg-color: #1a1a1a;
    --text-color: #e0e0e0;
    --item-bg: #2d2d2d;
    --filler-bg: #363636;
    --shadow-color: rgba(0, 0, 0, 0.3);
    --placeholder-color: #666;
    --heading-color: #ffffff;
  }

  :global([data-theme="light"]) {
    --bg-color: #ffffff;
    --text-color: #4a4a4a;
    --item-bg: #ffffff;
    --filler-bg: #f0f2f5;
    --shadow-color: rgba(0, 0, 0, 0.08);
    --placeholder-color: #9ba3af;
    --heading-color: #2d2d2d;
  }

  :global(body) {
    background-color: var(--bg-color);
    color: var(--text-color);
    transition: background-color 0.3s ease, color 0.3s ease;
    margin: 0;
    padding: 0;
    font-family: 'Plus Jakarta Sans', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  nav {
    background-color: var(--item-bg);
    box-shadow: 0 2px 8px var(--shadow-color);
    padding: 1rem 0;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 100;
  }

  .nav-content {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    margin: 0;
    font-size: 1.75rem;
    font-weight: 600;
    font-family: 'Outfit', sans-serif;
    color: var(--heading-color);
    letter-spacing: -0.02em;
  }

  .theme-toggle {
    background: none;
    border: none;
    color: var(--text-color);
    cursor: pointer;
    padding: 8px;
    border-radius: 50%;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: inherit;
  }

  .theme-toggle:hover {
    background-color: var(--filler-bg);
  }

  .container {
    display: flex;
    flex-direction: column;
    gap: 64px;
    max-width: 1200px;
    margin: 0 auto;
    padding: 120px 40px 60px 40px;
  }

  .item {
    display: flex;
    align-items: center;
    gap: 60px;
    background-color: var(--item-bg);
    border-radius: 12px;
    padding: 32px;
    box-shadow: 0 4px 12px var(--shadow-color);
    transition: all 0.3s ease-in-out;
  }

  .item:hover {
    transform: translateY(-6px);
    box-shadow: 0 8px 24px var(--shadow-color);
  }

  .filler-box {
    width: 400px;
    height: 600px;
    background: var(--filler-bg);
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 8px;
    overflow: hidden;
    position: relative;
  }

  .placeholder {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: var(--placeholder-color);
    opacity: 0;
    transition: opacity 0.3s ease;
  }

  .filler-box:not(:has(img[src])) .placeholder,
  .filler-box:has(img:not([src])) .placeholder {
    opacity: 1;
  }

  img {
    max-width: 100%;
    max-height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
    position: relative;
    z-index: 1;
  }

  img[src=""],
  img:not([src]) {
    opacity: 0;
  }

  .text-box {
    flex: 1;
    padding: 20px;
  }

  .text-box p {
    color: var(--text-color);
    font-size: 1.1rem;
    line-height: 1.7;
    margin: 0;
    font-weight: 400;
    letter-spacing: 0.01em;
  }
</style>