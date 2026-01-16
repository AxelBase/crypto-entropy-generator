<script lang="ts">
  import '../app.css';
  import { base } from '$app/paths';
  import { slide, fade, scale } from 'svelte/transition';
  import { quintOut } from 'svelte/easing';
  import { fly } from 'svelte/transition';

  let isDarkMode = false;
  function toggleTheme() {
    isDarkMode = !isDarkMode;
    document.body.dataset.bsTheme = isDarkMode ? 'dark' : 'light';
  }

  let isDropdownOpen = false;

  function toggleDropdown() { isDropdownOpen = !isDropdownOpen; }
  function closeDropdown() { isDropdownOpen = false; }

  function clickOutside(node: HTMLElement) {
    const handleClick = (event: MouseEvent) => {
      if (node && !node.contains(event.target as Node)) {
        node.dispatchEvent(new CustomEvent('click_outside'));
      }
    };
    document.addEventListener('click', handleClick, true);
    return {
      destroy() { document.removeEventListener('click', handleClick, true); }
    };
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

      <!-- Buy Me a Coffee + Bitcoin Dropdown (File 1 style adapted) -->
      <div class="position-relative ms-2" use:clickOutside on:click_outside={closeDropdown}>
        <button
          class="btn-coffee-premium d-flex align-items-center gap-2 shadow-sm"
          on:click={toggleDropdown}
          aria-label="Support options"
        >
          <i class="bi bi-cup-hot-fill"></i>
          <span class="d-none d-sm-inline fw-bold">Coffee</span>
        </button>

        {#if isDropdownOpen}
          <div 
            class="bmac-dropdown glass mt-2 shadow-lg" 
            transition:fly={{ y: -8, duration: 220 }}
          >
            <a 
              href="https://buymeacoffee.com/axelbase" 
              target="_blank" 
              rel="noopener" 
              on:click={closeDropdown}
            >
              <span class="amount">$3</span> One Coffee
            </a>
            <a 
              href="https://buymeacoffee.com/axelbase" 
              target="_blank" 
              rel="noopener" 
              on:click={closeDropdown}
            >
              <span class="amount">$5</span> Two Coffees
            </a>
            <a 
              href="https://buymeacoffee.com/axelbase" 
              target="_blank" 
              rel="noopener" 
              on:click={closeDropdown}
            >
              <span class="amount">$10</span> Three Coffees
            </a>

            <a 
              href="https://buymeacoffee.com/axelbase" 
              target="_blank" 
              rel="noopener" 
              on:click={closeDropdown} 
              class="custom-amount"
            >
              Custom Amount
            </a>

            <a
              href="bitcoin:bc1q3p0e6vt492m4w4fpz5m2cl4zcfuqqkgaj6myc9?label=AxelBase&message=Buy%20me%20a%20coffee"
              on:click={closeDropdown}
              class="custom-amount bitcoin-option"
            >
              Buy via Crypto (Bitcoin)
            </a>
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
    <span class="fw-semibold text-muted">© {new Date().getFullYear()} AxelBase Crypto Entropy Generator</span>
    <div class="d-flex gap-4">
      <a href="{base}/privacy" class="footer-link">Privacy Policy</a>
      <a href="{base}/terms" class="footer-link">Terms</a>
    </div>
  </div>
</footer>

<style>
  /* ── Previous styles kept ── */
  .logo-group:hover .nav-logo { transform: rotate(15deg) scale(1.15); }
  .fw-800 { font-weight: 800; }
  .nav-link-custom { font-weight: 700; color: var(--color-text-main); text-decoration: none; padding: 5px 12px; transition: 0.3s; position: relative; }
  .nav-link-custom:hover { color: var(--color-accent); }
  .nav-link-custom::after { content: ''; position: absolute; width: 0; height: 2px; bottom: 0; left: 50%; background: var(--color-accent); transition: 0.3s; transform: translateX(-50%); }
  .nav-link-custom:hover::after { width: 80%; }

  .footer-link { text-decoration: none; color: var(--color-text-muted); font-weight: 600; transition: 0.3s; }
  .footer-link:hover { color: var(--color-accent); }

  /* ── New & Adapted Coffee Button + Dropdown ── */
  .btn-coffee-premium {
    background: #ffdd00;
    color: #1a2a2a;
    font-weight: 800;
    border: none;
    border-radius: 50px;
    padding: 8px 18px;
    transition: all 0.28s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    box-shadow: 0 4px 12px rgba(255, 221, 0, 0.28);
  }

  .btn-coffee-premium:hover {
    transform: translateY(-2px) scale(1.06);
    background: #ffe54c;
    box-shadow: 0 10px 24px rgba(255, 221, 0, 0.45);
  }

  .bmac-dropdown {
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translateX(-50%);
    width: 240px;
    background: var(--glass-bg);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 1px solid var(--glass-border);
    border-radius: 20px;
    box-shadow: var(--glass-shadow);
    overflow: hidden;
    z-index: 1000;
    color: var(--color-text-main);
  }

  .bmac-dropdown a {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 12px 20px;
    color: var(--color-text-main);
    text-decoration: none;
    font-size: 0.96rem;
    transition: all 0.22s ease;
  }

  .bmac-dropdown a:hover {
    background: rgba(78, 186, 186, 0.15);
    color: var(--color-accent);
    padding-left: 28px;
  }

  .bmac-dropdown .amount {
    font-weight: 800;
    color: var(--color-accent);
    font-size: 1.12rem;
  }

  .bmac-dropdown .custom-amount {
    font-weight: 700;
    color: var(--color-accent);
    border-top: 1px solid var(--glass-border);
    justify-content: center !important;
    padding: 14px 20px;
  }

  .bitcoin-option {
    color: #f7931a !important;
    font-weight: 700;
  }

  .bitcoin-option:hover {
    background: rgba(247, 147, 26, 0.12) !important;
    color: #f7931a !important;
  }
</style>