<!-- src/routes/terms/+page.svelte -->
<script lang="ts">
  import { base } from '$app/paths';
</script>

<svelte:head>
  <title>Terms and Conditions | Crypto Offline Entropy Generator</title>
  <meta name="description" content="Terms of use for the Crypto Offline Entropy Generator — a free, open-source, client-side tool provided as-is with no warranties." />
  <meta property="og:title" content="Terms and Conditions | Crypto Offline Entropy Generator" />
  <meta property="og:description" content="Terms of use for the Crypto Offline Entropy Generator — a free, open-source, client-side tool provided as-is with no warranties." />
  <meta property="og:url" content="{base}/terms" />
  <meta property="og:type" content="website" />
  <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<div class="container fade-in post-layout" style="padding-top: 150px;">
  <div class="breadcrumbs">
    <a href="{base}/">Home</a>
    <span>/</span>
    <p>Terms and Conditions</p>
  </div>

  <article class="prose">
    <h1>Terms and Conditions</h1>

    <p class="post-meta">Effective Date: December 29, 2025</p>

    <h2>1. Acceptance of Terms</h2>
    <p>By accessing or using the <strong>Crypto Offline Entropy Generator</strong> ("the Tool"), you agree to be bound by these Terms and Conditions ("Terms"). If you do not agree, do not use the Tool. These Terms constitute a legally binding agreement between you and the developers of the Tool.</p>

    <h2>2. Description of the Tool</h2>
    <p>The Tool is a free, open-source, client-side web utility that generates cryptographically secure entropy using the browser’s Web Crypto API and converts it into various formats including hexadecimal, Base64, BIP39 mnemonic phrases, and Diceware-style passphrases. It also supports BIP39 validation and passphrase-derived entropy modes. All processing occurs locally in your browser.</p>

    <h2>3. No Data Collection</h2>
    <p>As stated in our Privacy Policy, the Tool collects <strong>zero personal data</strong>. No entropy, mnemonics, passphrases, IP addresses, or usage information is transmitted to us or any third party. You are solely responsible for any outputs you generate and any subsequent use of those outputs.</p>

    <h2>4. No Warranty</h2>
    <p>The Tool is provided <strong>"as is"</strong> and <strong>"as available"</strong> without any warranties of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, non-infringement, accuracy, reliability, or security. We do not guarantee that the Tool will meet your requirements, operate error-free, or produce cryptographically perfect randomness in every environment.</p>

    <h2>5. Limitation of Liability</h2>
    <p>To the fullest extent permitted by law, we shall not be liable for any direct, indirect, incidental, special, consequential, or punitive damages arising from your use of or inability to use the Tool, including but not limited to loss of funds, loss of data, personal injury, property damage, or any financial loss resulting from reliance on generated entropy, mnemonics, or passphrases.</p>

    <h2>6. User Responsibility</h2>
    <p>You are solely responsible for:</p>
    <ul>
      <li>Verifying that your browser supports the Web Crypto API before generating sensitive material.</li>
      <li>Securely storing and protecting any seeds, mnemonics, or keys you generate.</li>
      <li>Ensuring you use the Tool in a trusted, offline environment for high-value operations.</li>
      <li>Understanding the risks of brainwallet/passphrase modes and never using weak passphrases.</li>
    </ul>
    <p><strong>Never</strong> use outputs from this Tool for real funds without independent verification and testing with negligible amounts first.</p>

    <h2>7. Prohibited Use</h2>
    <p>You may not use the Tool for any unlawful purpose or in any way that violates applicable laws. You may not attempt to reverse-engineer, decompile, or extract source code beyond what is publicly available under the open-source license.</p>

    <h2>8. Open-Source License</h2>
    <p>The Tool is released under the MIT License (or equivalent open-source license as indicated in the repository). You are free to use, modify, and distribute the code in accordance with that license. These Terms apply only to the hosted service at this domain.</p>

    <h2>9. Changes to Terms</h2>
    <p>We may update these Terms at any time. Changes will be posted on this page with an updated effective date. Continued use after changes constitutes acceptance of the revised Terms.</p>

    <h2>10. Governing Law</h2>
    <p>These Terms shall be governed by the laws of the jurisdiction where the developers reside, without regard to conflict of law principles.</p>

    <h2>11. Contact</h2>
    <p>For questions regarding these Terms, please open an issue on the project’s public GitHub repository.</p>

    <p class="italic-note">This is a free, no-liability tool provided for educational and personal use. Always treat generated seeds as extremely sensitive and never rely solely on any single source.</p>
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