<!-- src/routes/privacy/+page.svelte -->
<script lang="ts">
  import { base } from '$app/paths';
</script>

<svelte:head>
  <title>Privacy Policy | Crypto Offline Entropy Generator</title>
  <meta name="description" content="Our commitment to zero data collection: the Crypto Offline Entropy Generator runs entirely in your browser and never sends any information to servers." />
  <meta property="og:title" content="Privacy Policy | Crypto Offline Entropy Generator" />
  <meta property="og:description" content="Our commitment to zero data collection: the Crypto Offline Entropy Generator runs entirely in your browser and never sends any information to servers." />
  <meta property="og:url" content="{base}/privacy" />
  <meta property="og:type" content="website" />
  <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<div class="container fade-in post-layout" style="padding-top: 150px;">
  <div class="breadcrumbs">
    <a href="{base}/">Home</a>
    <span>/</span>
    <p>Privacy Policy</p>
  </div>

  <article class="prose">
    <h1>Privacy Policy</h1>

    <p class="post-meta">Effective Date: December 29, 2025</p>

    <h2>1. Introduction</h2>
    <p>Welcome to the <strong>Crypto Offline Entropy Generator</strong>, a fully client-side, open-source web utility designed to generate cryptographically secure entropy and BIP39 mnemonic phrases. We, the developers ("we," "us," or "our"), are committed to protecting your privacy. This tool operates entirely within your browser using the Web Crypto API and requires no account, login, or personal information. <strong>We do not collect, store, transmit, or process any data from you</strong>. This Privacy Policy explains our zero-data-collection approach in detail.</p>

    <h2>2. Information We Do Not Collect</h2>
    <p>Because the generator runs exclusively on your device, we never receive or record any of the following:</p>
    <ul>
      <li><strong>Personal Identifiable Information (PII)</strong> — names, email addresses, wallet addresses, phone numbers, or any other identifying data.</li>
      <li><strong>Generated Entropy or Mnemonics</strong> — the random bytes, hex strings, Base64 outputs, BIP39 phrases, or Diceware passphrases you create stay only in your browser.</li>
      <li><strong>Input Data</strong> — passphrases entered in brainwallet modes are processed locally and never leave your device.</li>
      <li><strong>Technical or Usage Data</strong> — we do not log IP addresses, browser fingerprints, device information, timestamps, or session duration.</li>
      <li><strong>Analytics or Tracking</strong> — no cookies, pixels, beacons, Google Analytics, or any third-party tracking is used.</li>
    </ul>
    <p>All operations — from random number generation to mnemonic conversion and validation — happen <strong>client-side only</strong>. Your entropy never touches our servers or any external service.</p>

    <h2>3. How the Tool Works</h2>
    <p>When you use the Crypto Offline Entropy Generator:</p>
    <ul>
      <li><strong>Randomness Generation</strong> — <code>window.crypto.getRandomValues()</code> pulls entropy directly from your operating system’s secure random source.</li>
      <li><strong>Processing</strong> — conversions to hex, Base64, BIP39, and Diceware occur locally using pure JavaScript in your browser.</li>
      <li><strong>Validation & Recovery</strong> — BIP39 mnemonic validation and entropy recovery are performed entirely client-side.</li>
      <li><strong>Clipboard & Export</strong> — copy-to-clipboard and any manual export actions are handled by your browser’s native APIs.</li>
    </ul>
    <p>No data is sent to us or any third party. Temporary browser memory used during your session is cleared when you close the tab or refresh the page.</p>

    <h2>4. Third-Party Services</h2>
    <p>We do not integrate analytics, advertising, or any external APIs that collect data. The tool uses only browser-native APIs (Web Crypto) and open-source JavaScript libraries loaded from trusted CDNs or bundled statically. These libraries do not track users or send data anywhere.</p>

    <h2>5. Cookies and Tracking Technologies</h2>
    <p><strong>No cookies are used</strong>. The site is completely stateless. No tracking pixels, localStorage, sessionStorage, or IndexedDB is employed for tracking purposes. Your session is ephemeral and disappears when you leave the page.</p>

    <h2>6. Data Security</h2>
    <p>Although we collect no data, security still depends on your environment:</p>
    <ul>
      <li>Use the tool in offline/air-gapped mode for maximum protection.</li>
      <li>Never screenshot or photograph sensitive outputs.</li>
      <li>Keep your browser and operating system updated.</li>
      <li>Store generated seeds securely offline (metal backups recommended).</li>
    </ul>

    <h2>7. Children’s Privacy</h2>
    <p>This tool is not directed to children under 13. We do not knowingly collect data from anyone under 13. If you believe a child has used the tool, please contact us.</p>

    <h2>8. International Users & Compliance</h2>
    <p>Because no personal data is collected, the tool complies by design with major privacy regulations including <strong>GDPR</strong>, <strong>CCPA/CPRA</strong>, <strong>Brazil LGPD</strong>, and others. There is no personal data processing to report.</p>

    <h2>9. Changes to This Policy</h2>
    <p>We may update this Privacy Policy to reflect changes in the tool or legal requirements. Updates will be posted here with a revised effective date. Continued use constitutes acceptance of the updated policy.</p>

    <h2>10. Contact</h2>
    <p>For questions about this Privacy Policy, contact us via the project’s public GitHub repository issues page.</p>

    <p class="italic-note">We are proud to offer a truly <strong>zero-data-collection</strong> tool. Your entropy, mnemonics, and passphrases remain yours alone.</p>
  </article>
</div>

<style>
  .post-layout {
    max-width: 800px;
    padding-top: 2rem;
    padding-bottom: 4rem;
  }

  .breadcrumbs {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
    font-size: 0.9rem;
    color: var(--color-text-muted);
  }

  .breadcrumbs a {
    color: var(--color-accent);
    text-decoration: none;
    transition: color 0.3s ease;
  }

  .breadcrumbs a:hover {
    text-decoration: underline;
    color: var(--color-accent-hover);
  }

  .breadcrumbs p {
    margin: 0;
  }

  .prose {
    line-height: 1.8;
    color: var(--color-text-main);
  }

  .prose .post-meta {
    color: var(--color-text-muted);
    font-size: 0.9rem;
    margin-bottom: 2rem;
    border-bottom: 1px solid var(--glass-border);
    padding-bottom: 1rem;
  }

  .prose h1,
  .prose h2{
    color: var(--color-accent);
    font-weight: 700;
  }

  .prose h1 {
    font-size: 2.5rem;
    margin-bottom: 0.5rem;
  }

  .prose h2 {
    font-size: 1.8rem;
    margin-top: 2.5rem;
    margin-bottom: 1rem;
    border-bottom: 1px solid var(--glass-border);
    padding-bottom: 0.5rem;
  }

  .prose p {
    margin-bottom: 1.25rem;
    color: var(--color-text-main);
  }

  .prose ul {
    list-style-type: '→ ';
    padding-left: 1.5rem;
    margin-bottom: 1.25rem;
    color: var(--color-text-main);
  }

  .prose ul li::marker {
    color: var(--color-accent);
  }

  .prose ul li {
    padding-left: 0.5rem;
    margin-bottom: 0.75rem;
  }

  .prose .italic-note {
    font-style: italic;
    color: var(--color-text-muted);
    text-align: center;
    margin-top: 3rem;
    font-size: 1.05rem;
  }
</style>