<script>
  import { generateFromMode } from '$lib/entropyLogic.js';
  import { onMount } from 'svelte';
  import { browser } from '$app/environment';
  import { fade, fly, slide, scale } from 'svelte/transition';
  import { backOut } from 'svelte/easing';

  let entropy = null;
  let mode = 'device'; 
  let passphrase = '';
  let mnemonicInput = '';
  let selectedBits = 256;
  let loading = false;
  let copyStatus = {};

  const bitsOptions = [128, 160, 192, 224, 256];

  async function generate() {
    if (!browser) return;
    loading = true;
    try {
      entropy = await generateFromMode(mode, passphrase.trim(), selectedBits, mnemonicInput.trim());
    } catch (err) {
      entropy = null;
    }
    loading = false;
  }

  function copyToClipboard(text, key) {
    navigator.clipboard.writeText(text).then(() => {
      copyStatus[key] = true;
      setTimeout(() => copyStatus[key] = false, 2000);
    });
  }

  onMount(() => { generate(); });

  $: if (browser && mode !== 'validate') { mnemonicInput = ''; generate(); }
  $: if (browser && (mode === 'device' || mode === 'validate')) { passphrase = ''; }
  $: if (browser && mode !== 'device') generate();
</script>

<section id="home" class="container py-5 mt-5">
  <div class="row justify-content-center">
    <div class="col-xl-10 col-lg-11">
      <div class="text-center mb-5" in:fly={{ y: -20, duration: 800 }}>
        <h1 class="display-3 fw-800 mb-3 text-gradient">AxelBase Entropy</h1>
        <p class="lead text-muted mx-auto" style="max-width: 650px;">Industry-grade, client-side entropy generation for hardware wallets and secure keys.</p>
      </div>

      <div class="glass-card p-4 p-md-5" in:fly={{ y: 40, duration: 1000, delay: 200 }}>
        <div class="row g-4 align-items-end mb-4">
          <div class="col-lg-5">
            <label for="modeSelect" class="form-label fw-bold small text-uppercase mb-2 ms-2">Entropy Source</label>
            <select id="modeSelect" class="form-select form-select-lg" bind:value={mode} disabled={loading}>
              <option value="device">Device Entropy (CSPRNG)</option>
              <option value="passphrase">Passphrase Only (Brainwallet)</option>
              <option value="hybrid">Hybrid (Recommended)</option>
              <option value="validate">Validator Mode</option>
            </select>
          </div>

          {#if mode !== 'device'}
            <div class="col-lg-4" transition:slide={{ axis: 'x', duration: 400 }}>
              <label for="secretInput" class="form-label fw-bold small text-uppercase mb-2 ms-2">Input Secret</label>
              {#if mode === 'validate'}
                <textarea id="secretInput" class="form-control" rows="1" bind:value={mnemonicInput} placeholder="Paste phrase..."></textarea>
              {:else}
                <input id="secretInput" type="password" class="form-control form-control-lg" bind:value={passphrase} placeholder="Strong secret...">
              {/if}
            </div>
          {/if}

          <div class="col-lg-1">
            <label for="bitsSelect" class="form-label fw-bold small text-uppercase mb-2 ms-2">Bits</label>
            <select id="bitsSelect" class="form-select form-select-lg" bind:value={selectedBits}>
              {#each bitsOptions as bits}
                <option value={bits}>{bits}</option>
              {/each}
            </select>
          </div>

          <div class="col-lg-2">
            <button class="btn btn-primary btn-lg w-100 py-3 fw-bold shadow-sm hover-lift" on:click={generate} disabled={loading}>
              {loading ? '...' : 'Generate'}
            </button>
          </div>
        </div>

        {#if entropy}
          <div class="mt-5 pt-4 border-top border-secondary border-opacity-10" transition:fade>
            <h4 class="fw-800 mb-4 d-flex align-items-center gap-2"><i class="bi bi-cpu-fill text-success"></i> Secure Output</h4>
            <div class="row g-4">
              {#each ['bip39', 'hex', 'diceware', 'base64'] as type}
                {#if entropy[type]}
                  <div class="col-12" in:scale={{ duration: 400, delay: 100, easing: backOut }}>
                    <div class="glass p-4 rounded-4 position-relative border-hover">
                      <div class="d-flex justify-content-between align-items-center mb-3">
                        <span class="fw-800 text-uppercase small text-muted tracking-wider">{type === 'bip39' ? 'Mnemonic (BIP39)' : type}</span>
                        <button class="btn-copy-action {copyStatus[type] ? 'copied' : ''}" on:click={() => copyToClipboard(entropy[type], type)}>
                          <i class="bi {copyStatus[type] ? 'bi-check-circle-fill' : 'bi-clipboard2-data'}"></i>
                          {copyStatus[type] ? 'Copied!' : 'Copy'}
                        </button>
                      </div>
                      <pre class="mb-0">{entropy[type]}</pre>
                    </div>
                  </div>
                {/if}
              {/each}
            </div>
          </div>
        {/if}
      </div>
    </div>
  </div>
</section>

<section id="about" class="section-block">
  <div class="container">
    <div class="row align-items-start g-5">
      <div class="col-lg-7" in:fade={{ duration: 1000 }}>
        <h2 class="display-4 fw-800 mb-4 text-gradient">About AxelBase</h2>
        <p class="lead fw-bold text-accent mb-4">Privacy and security as core principles.</p>
        <div class="text-muted pe-lg-4">
          <p>The Crypto Offline Entropy Generator is a free, open-source, fully client-side web utility designed to provide cryptographically secure randomness for generating cryptocurrency wallet seeds, private keys, and other sensitive cryptographic material.</p>
          <p>Built with privacy and security as core principles, the tool operates entirely within your browser using the native Web Crypto API, ensuring that no data—entropy, mnemonics, passphrases, or usage information—ever leaves your device or is transmitted to any server.</p>
          <p>Unlike online seed generators that pose risks of interception or logging, this tool requires no account, no network requests after initial page load, and no third-party analytics or tracking. All randomness is sourced directly from your operating system’s secure entropy pool via <code>window.crypto.getRandomValues()</code>, the industry-standard method for cryptographic randomness in modern browsers.</p>
          <p>Advanced users benefit from brainwallet capabilities. Passphrase-only mode derives deterministic entropy from a user-provided phrase using SHA-256, while Hybrid mode combines the passphrase with fresh device randomness via HMAC-SHA512.</p>
        </div>
      </div>
      <div class="col-lg-5 sticky-lg-top" style="top: 120px;">
        <div class="glass-card p-5 shadow-lg border-hover">
          <div class="text-center mb-4">
            <i class="bi bi-shield-fill-check display-1 text-primary mb-3"></i>
            <h3 class="fw-bold">Zero-Knowledge</h3>
            <p class="text-muted">No server, no logs, no leaks. Everything resides in a single client-side file.</p>
          </div>
          <hr class="my-4 opacity-10">
          <div class="d-flex align-items-center gap-3 mb-3">
            <i class="bi bi-check2-circle text-success fs-4"></i>
            <span class="fw-600">Pure CSPRNG Randomness</span>
          </div>
          <div class="d-flex align-items-center gap-3 mb-3">
            <i class="bi bi-check2-circle text-success fs-4"></i>
            <span class="fw-600">BIP39 Compliant</span>
          </div>
          <div class="d-flex align-items-center gap-3">
            <i class="bi bi-check2-circle text-success fs-4"></i>
            <span class="fw-600">Air-Gap Compatible</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<section id="how-to-use" class="section-block">
  <div class="container">
    <div class="text-center mb-5">
      <h2 class="display-4 fw-800">Maximum Security Protocol</h2>
      <p class="text-muted">Follow these steps for secure cryptographic usage.</p>
    </div>
    
    <div class="row g-4">
      <div class="col-md-4">
        <div class="glass-card p-5 h-100 border-hover">
          <div class="display-3 fw-800 text-primary mb-3">01</div>
          <h5 class="fw-bold">Go Air-Gapped</h5>
          <p class="text-muted small">Load this page, then disconnect your internet. For critical funds, use a computer that never touches the web after loading this utility.</p>
        </div>
      </div>
      <div class="col-md-4">
        <div class="glass-card p-5 h-100 border-hover">
          <div class="display-3 fw-800 text-primary mb-3">02</div>
          <h5 class="fw-bold">Select Mode</h5>
          <p class="text-muted small">Use "Pure Device Entropy" (Default) for maximum randomness or "Hybrid" to mix in a memorable passphrase for extra protection.</p>
        </div>
      </div>
      <div class="col-md-4">
        <div class="glass-card p-5 h-100 border-hover">
          <div class="display-3 fw-800 text-primary mb-3">03</div>
          <h5 class="fw-bold">Physical Storage</h5>
          <p class="text-muted small">Write the words on paper or metal backups. Never screenshot or store digital copies on connected devices or cloud services.</p>
        </div>
      </div>
    </div>

    <div class="mt-5 p-4 glass rounded-4 border-hover">
      <p class="mb-0 text-muted small text-center italic">
        <i class="bi bi-info-circle me-2"></i>
        <strong>Security Tip:</strong> To verify an existing backup, use <strong>Validator Mode</strong>. Paste your phrase to check checksum validity and recover original entropy.
      </p>
    </div>
  </div>
</section>

<section id="faq" class="section-block">
  <div class="container">
    <h2 class="text-center display-4 fw-800 mb-5">Frequently Asked</h2>
    <div class="accordion accordion-flush mx-auto" style="max-width: 900px;" id="faqAcc">
      
      <div class="accordion-item glass border-0 rounded-4 mb-3 overflow-hidden">
        <h2 class="accordion-header">
          <button class="accordion-button collapsed bg-transparent fw-bold p-4 fs-5" type="button" data-bs-toggle="collapse" data-bs-target="#q1">
            Is this tool truly offline and private?
          </button>
        </h2>
        <div id="q1" class="accordion-collapse collapse" data-bs-parent="#faqAcc">
          <div class="accordion-body text-muted px-4 pb-4">
            Yes. After the initial page load, no network requests are made. All randomness, processing, and validation occur exclusively in your browser using the Web Crypto API. We collect zero data—no analytics, cookies, IP logging, or transmission of entropy/mnemonics.
          </div>
        </div>
      </div>

      <div class="accordion-item glass border-0 rounded-4 mb-3 overflow-hidden">
        <h2 class="accordion-header">
          <button class="accordion-button collapsed bg-transparent fw-bold p-4 fs-5" type="button" data-bs-toggle="collapse" data-bs-target="#q2">
            Why should I trust browser randomness?
          </button>
        </h2>
        <div id="q2" class="accordion-collapse collapse" data-bs-parent="#faqAcc">
          <div class="accordion-body text-muted px-4 pb-4">
            The Web Crypto API’s <code>getRandomValues()</code> method draws from your operating system’s cryptographically secure entropy pool (e.g., <code>/dev/urandom</code> on Linux, <code>CryptGenRandom</code> on Windows). This is the gold standard for client-side randomness.
          </div>
        </div>
      </div>

      <div class="accordion-item glass border-0 rounded-4 mb-3 overflow-hidden">
        <h2 class="accordion-header">
          <button class="accordion-button collapsed bg-transparent fw-bold p-4 fs-5" type="button" data-bs-toggle="collapse" data-bs-target="#q3">
            Are brainwallet modes safe?
          </button>
        </h2>
        <div id="q3" class="accordion-collapse collapse" data-bs-parent="#faqAcc">
          <div class="accordion-body text-muted px-4 pb-4">
            Passphrase-only mode is convenient but risky if using weak phrases—dictionary attacks are a threat. Hybrid mode is safer, combining your passphrase with device randomness. Pure device entropy remains the most secure option.
          </div>
        </div>
      </div>

      <div class="accordion-item glass border-0 rounded-4 mb-3 overflow-hidden">
        <h2 class="accordion-header">
          <button class="accordion-button collapsed bg-transparent fw-bold p-4 fs-5" type="button" data-bs-toggle="collapse" data-bs-target="#q4">
            Should I screenshot my seed?
          </button>
        </h2>
        <div id="q4" class="accordion-collapse collapse" data-bs-parent="#faqAcc">
          <div class="accordion-body text-muted px-4 pb-4">
            <strong>Never.</strong> Screenshots create vulnerable digital copies prone to malware exfiltration. Transcribe manually onto paper or metal backups stored in secure locations.
          </div>
        </div>
      </div>

    </div>
  </div>
</section>

<style>
  :global(html) { scroll-behavior: smooth; scroll-padding-top: 100px; }
  .fw-600 { font-weight: 600; }
  .fw-800 { font-weight: 800; }
  .text-accent { color: var(--color-accent); }
  .text-gradient { background: linear-gradient(135deg, var(--primary-opal), var(--color-accent)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
  .hover-lift { transition: 0.3s; }
  .hover-lift:hover { transform: translateY(-3px); box-shadow: 0 10px 20px rgba(0,0,0,0.1); }
  .border-hover:hover { border-color: var(--color-accent) !important; }
  .accordion-button:not(.collapsed) { color: var(--color-accent); box-shadow: none; }
  .italic { font-style: italic; }
  .tracking-wider { letter-spacing: 0.05em; }
</style>