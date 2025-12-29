<!-- src/routes/blog/+page.svelte -->
<script lang="ts">
  import { base } from '$app/paths';

  const posts = [
    { href: '/blog/posts/post1', title: 'Generating Secure Entropy with Web Crypto API', description: 'How the tool uses browser-native cryptographically secure randomness from system entropy sources.' },
    { href: '/blog/posts/post2', title: 'Understanding BIP39 Mnemonic Phrases', description: 'The standard process of converting entropy to 12-24 word seed phrases, including checksum calculation.' },
    { href: '/blog/posts/post3', title: 'Validating and Recovering BIP39 Seeds', description: 'How checksum verification works and recovering raw entropy from an existing mnemonic.' },
    { href: '/blog/posts/post4', title: 'Brainwallet Modes: Passphrase-Derived Entropy', description: 'Exploring deterministic generation from passphrases and the hybrid approach combining device randomness.' },
    { href: '/blog/posts/post5', title: 'Risks and Limitations of Brainwallets', description: 'Why passphrase-only methods are vulnerable to brute-force attacks and when to avoid them.' },
    { href: '/blog/posts/post6', title: 'Best Practices for Offline Seed Generation', description: 'Recommendations for air-gapped use and maximizing security when creating cryptographic keys.' },
    { href: '/blog/posts/post7', title: 'Entropy Strength: 128 vs 256 Bits Explained', description: 'Comparing security levels and how the tool supports configurable entropy sizes.' },
  ];
</script>

<svelte:head>
  <title>Blog | Offline Entropy Insights</title>
  <meta name="description" content="Technical articles on cryptographic entropy generation, BIP39 standards, offline security, and best practices for the Crypto Offline Entropy Generator." />
</svelte:head>

<div class="container fade-in blog-index" style="padding-top: 150px;">
  <header class="blog-header">
    <h1><i class="bi bi-shield-lock"></i> Blog: Offline Entropy Insights</h1>
    <p class="subtitle">
      In-depth technical guides on cryptographic randomness, BIP39 standards, entropy sources, and secure offline practices for generating cryptocurrency seeds and keys.
    </p>
  </header>

  <div class="posts-grid">
    {#each posts as post}
      <a href="{base}{post.href}" class="card post-card">
        <div class="card-body">
          <h2 class="post-title">{post.title}</h2>
          <p class="post-description">{post.description}</p>
          <span class="read-more">Read Article &rarr;</span>
        </div>
      </a>
    {/each}
  </div>
</div>

<style>
  .blog-index {
    padding-top: 2rem;
    padding-bottom: 4rem;
  }

  .blog-header {
    text-align: center;
    margin-bottom: 3rem;
    border-bottom: 1px solid var(--glass-border);
    padding-bottom: 2rem;
  }

  .blog-header h1 {
    font-size: 2.8rem;
    margin-bottom: 1rem;
    color: var(--color-text-main);
    font-weight: 800;
  }

  .subtitle {
    font-size: 1.1rem;
    color: var(--color-text-muted);
    max-width: 700px;
    margin: 0 auto;
    line-height: 1.7;
  }

  .posts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
  }

  .post-card {
    background: var(--glass-bg);
    backdrop-filter: blur(25px);
    -webkit-backdrop-filter: blur(25px);
    border: 1px solid var(--glass-border);
    border-radius: 35px;
    box-shadow: var(--glass-shadow);
    text-decoration: none;
    overflow: hidden;
    transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    display: flex;
    flex-direction: column;
  }

  .post-card:hover {
    transform: translateY(-12px) scale(1.01);
    box-shadow: 0 30px 70px rgba(0, 0, 0, 0.2);
    border-color: var(--color-accent);
  }

  .post-card .card-body {
    padding: 1.8rem;
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  .post-title {
    font-size: 1.25rem;
    color: var(--color-accent);
    font-weight: 700;
    margin-bottom: 0.75rem;
    line-height: 1.4;
  }

  .post-description {
    color: var(--color-text-muted);
    flex-grow: 1;
    margin-bottom: 1.5rem;
    line-height: 1.6;
  }

  .read-more {
    color: var(--color-accent);
    font-weight: 700;
    font-size: 1rem;
    align-self: flex-start;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .read-more::after {
    content: '→';
    font-size: 1.2rem;
    transition: transform 0.3s ease;
  }

  .post-card:hover .read-more::after {
    transform: translateX(8px);
  }
</style>