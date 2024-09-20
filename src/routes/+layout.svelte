<script>
  import "@fontsource/averia-serif-libre";
  import "../app.css";

  export let title = "Night Skies ✨";
  export let author = "Javi Zaleta";
  export let description = "Night skies with shooting stars and lofi beats";
  export let url = "https://night-skies.pages.dev";
  export let image = "https://github.com/jzaleta.png";
</script>

<svelte:head>
  <!-- Basic Meta Tags -->
  <title>{title}</title>
  <meta name="description" content={description} />
  <meta name="author" content={author} />

  <!-- OG Meta Tags -->
  <meta property="og:type" content="website" />
  <meta property="og:url" content={url} />
  <meta property="og:title" content={title} />
  <meta property="og:description" content={description} />
  <meta property="og:image" content={image} />

  <meta property="og:site_name" content={title} />
  <meta property="og:locale" content="en_US" />

  <!-- X/Twitter Meta Tags -->
  <meta property="twitter:card" content="summary_large_image" />
  <meta property="twitter:url" content={url} />
  <meta property="twitter:title" content={title} />
  <meta property="twitter:description" content={description} />
  <meta name="twitter:image" content={image} />

  <!-- Favicon Meta Tags -->
  <link rel="apple-touch-icon" sizes="180x180" href="/favicon.png" />
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon.png" />
  <link rel="icon" type="image/png" sizes="16x16" href="/favicon.png" />
</svelte:head>

<slot />
