<script>
  import { onMount } from 'svelte';
  import FontDisplay from './FontDisplay.svelte';
  import Footer from './Footer.svelte';

  let fonts = [];
  let randomFont = null;

  async function fetchFonts() {
    const response = await fetch(`https://www.googleapis.com/webfonts/v1/webfonts?key=${process.env.GOOGLE_FONTS_API_KEY}`);
    const data = await response.json();
    fonts = data.items;
    getRandomFont();
  }

  function getRandomFont() {
    const index = Math.floor(Math.random() * fonts.length);
    randomFont = fonts[index];
  }

  onMount(() => {
    fetchFonts();
  });
</script>

<main>
  <h1>Random Google Font Generator</h1>
  {#if randomFont}
    <div class="card">
      <FontDisplay {randomFont} getRandomFont={getRandomFont} />
    </div>
  {:else}
    <p>Loading fonts...</p>
  {/if}
</main>
<Footer/>




<style>
    main {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: #15202B; 
        color: #FFF;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        padding: 20px;
        box-sizing: border-box;
    }

    h1 {
        font-size: 2rem;
		margin-top: 2rem;
        margin-bottom: 2rem;
        color: #1DA1F2; 
    }

    .card {
        background-color: #253341;
        border-radius: 15px;
        padding: 20px;
        margin: 20px 0;
        width: 80%;
        max-width: 600px;
    }
</style>
