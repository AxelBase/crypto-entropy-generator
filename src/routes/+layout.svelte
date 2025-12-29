<script lang="ts">
  import '../app.css';
  import { base } from '$app/paths';
  import { slide, fade, scale } from 'svelte/transition';
  import { quintOut } from 'svelte/easing';

  let isDarkMode = false;
  function toggleTheme() {
    isDarkMode = !isDarkMode;
    document.body.dataset.bsTheme = isDarkMode ? 'dark' : 'light';
  }

  const paypalUsername = 'AxelLab427';
  const donationAmounts = [1, 3, 5, 10];
  let isDropdownOpen = false;

  function clickOutside(node: HTMLElement) {
    const handleClick = (event: MouseEvent) => {
      if (node && !node.contains(event.target as Node)) node.dispatchEvent(new CustomEvent('click_outside'));
    };
    document.addEventListener('click', handleClick, true);
    return { destroy() { document.removeEventListener('click', handleClick, true); } };
  }
</script>

<header class="fixed-top p-3 w-100" style="z-index: 1050;">
  <nav class="container glass rounded-pill px-4 py-2 d-flex justify-content-between align-items-center shadow-lg" style="max-width: 1200px; backdrop-filter: blur(20px);">
    
    <div class="d-flex align-items-center gap-2">
      <a href="{base}/" class="d-flex align-items-center gap-2 text-decoration-none logo-group">
        <img src="{base}/AxelLab-Logo.ico" alt="Logo" class="nav-logo" style="height: 38px; transition: 0.5s ease;" />
        <span class="fw-800 fs-5 d-none d-md-inline" style="color: var(--color-text-main);">AxelBase</span>
      </a>

      <button class="btn border-0 p-2 theme-toggle-btn ms-2" on:click={toggleTheme} aria-label="Toggle Theme">
        {#key isDarkMode}
          <div in:scale={{ duration: 400, easing: quintOut }}>
            <i class="bi {isDarkMode ? 'bi-sun-fill text-warning' : 'bi-moon-stars-fill text-primary'} fs-5"></i>
          </div>
        {/key}
      </button>

      <div class="position-relative ms-1" use:clickOutside on:click_outside={() => isDropdownOpen = false}>
        <button class="btn btn-coffee d-flex align-items-center gap-2" on:click={() => isDropdownOpen = !isDropdownOpen}>
          <i class="bi bi-cup-hot-fill"></i>
          <span class="d-none d-sm-inline">Coffee</span>
        </button>
        {#if isDropdownOpen}
          <div class="dropdown-menu-custom glass p-2 mt-2 shadow-lg" transition:slide={{ duration: 300 }}>
            {#each donationAmounts as amount}
              <a href="https://paypal.me/{paypalUsername}/{amount}" target="_blank" class="donation-link">${amount}</a>
            {/each}
          </div>
        {/if}
      </div>
    </div>

    <ul class="nav d-none d-lg-flex align-items-center gap-3">
      <li><a class="nav-link-custom" href="{base}/">Home</a></li>
      <li><a class="nav-link-custom" href="{base}/#about">About</a></li>
      <li><a class="nav-link-custom" href="{base}/#how-to-use">How to Use</a></li>
      <li><a class="nav-link-custom" href="{base}/#faq">FAQ</a></li>
      <li><a class="btn btn-primary btn-sm px-4 rounded-pill fw-bold shadow-sm" href="{base}/blog">Blog</a></li>
    </ul>
  </nav>
</header>

<main>
  <slot />
</main>

<footer class="glass border-top py-5 mt-5">
  <div class="container d-flex flex-column flex-md-row justify-content-between align-items-center gap-3">
    <span class="fw-semibold text-muted">&copy; {new Date().getFullYear()} AxelBase Crypto Entropy Generator</span>
    <div class="d-flex gap-4">
      <a href="{base}/privacy" class="footer-link">Privacy Policy</a>
      <a href="{base}/terms" class="footer-link">Terms</a>
    </div>
  </div>
</footer>

<style>
  .logo-group:hover .nav-logo { transform: rotate(15deg) scale(1.15); }
  .fw-800 { font-weight: 800; }
  .nav-link-custom { font-weight: 700; color: var(--color-text-main); text-decoration: none; padding: 5px 12px; transition: 0.3s; position: relative; }
  .nav-link-custom:hover { color: var(--color-accent); }
  .nav-link-custom::after { content: ''; position: absolute; width: 0; height: 2px; bottom: 0; left: 50%; background: var(--color-accent); transition: 0.3s; transform: translateX(-50%); }
  .nav-link-custom:hover::after { width: 80%; }
  
  .btn-coffee { background: #ffdd00; color: #333; font-weight: 800; border: none; border-radius: 50px; padding: 7px 20px; transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
  .btn-coffee:hover { transform: scale(1.1) rotate(-3deg); background: #ffe54c; box-shadow: 0 10px 20px rgba(255, 221, 0, 0.3); }

  .dropdown-menu-custom { position: absolute; top: 100%; left: 0; min-width: 120px; border-radius: 20px; z-index: 1000; }
  .donation-link { display: block; text-align: center; padding: 12px; font-weight: 800; text-decoration: none; color: var(--color-text-main); border-radius: 14px; transition: 0.2s; }
  .donation-link:hover { background: var(--color-accent); color: white; }

  .footer-link { text-decoration: none; color: var(--color-text-muted); font-weight: 600; transition: 0.3s; }
  .footer-link:hover { color: var(--color-accent); }
</style>