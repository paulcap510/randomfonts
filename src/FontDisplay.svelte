<script>
  import CopyToClipboard from 'svelte-copy-to-clipboard';
  export let randomFont;
  export let getRandomFont;
  
  $: if (randomFont) {
    const fontFamily = randomFont.family.replace(/\s+/g, '+');
    const fontUrl = `https://fonts.googleapis.com/css2?family=${fontFamily}&display=swap`;
    
    let existingLink = document.querySelector(`link[href="${fontUrl}"]`);
    if (!existingLink) {
      let link = document.createElement('link');
      link.href = fontUrl;
      link.rel = 'stylesheet';
      document.head.appendChild(link);
    }
    document.documentElement.style.setProperty('--dynamic-font', randomFont.family);
  }

  $: fontFamily = randomFont?.family.replace(/\s+/g, '+');
  $: htmlEmbedCode = `<link href="https://fonts.googleapis.com/css2?family=${fontFamily}&display=swap" rel="stylesheet">`;
  $: cssImportCode = `@import url('https://fonts.googleapis.com/css2?family=${fontFamily}&display=swap');`;
  $: cssFontFamily = `font-family: '${randomFont?.family}', sans-serif;`;

  function copyToClipboard(text) {
    navigator.clipboard.writeText(text).then(() => {
    }).catch(err => {
    });
  }
</script>


<div>
  <p class="intro-text">Ever want to use a new Google Font, but not sure which one to use? This random font generator will generate a random font for you using the Google Font API. Just click the 'Get Random Font' button below, and it will generate a new font for you on the screen! Click the clipboard icon to copy the code and just paste it where you want to use it.</p>
  <h2>Your font: {randomFont.family}</h2>
  <p>Font sample:</p>
  <p class="sample-text">The quick brown fox jumps over the lazy dog.</p>

  <p>Use this HTML to embed in your site:</p>
  <div class="code-container">
    <code>{htmlEmbedCode}</code>
    <i class="fas fa-copy clipboard-icon" on:click={() => copyToClipboard(htmlEmbedCode)}></i>
  </div>

  <p>Add this to your CSS:</p>
  <div class="code-container">
    <code>{cssImportCode}</code>
    <i class="fas fa-copy clipboard-icon" on:click={() => copyToClipboard(cssImportCode)}></i>
  </div>

  <p>And apply the font with this CSS:</p>
  <div class="code-container">
    <code>{cssFontFamily}</code>
    <i class="fas fa-copy clipboard-icon" on:click={() => copyToClipboard(cssFontFamily)}></i>
  </div>

  <div class="button-container">
    <button on:click={getRandomFont}>Get Random Font</button>
  </div>
</div>



<style>
  div {
    max-width: 600px; 
    margin: auto;
    padding: 20px;
    border-radius: 8px;
    overflow: hidden;
  }

  h2, p {
    margin: 10px 0;
  }


  .sample-text {
    display: block; 
    color: #1DA1F2;
    font-size: 1.55rem;
    font-family: var(--dynamic-font), sans-serif;
    overflow-wrap: break-word;
    max-height: 100px; 
    overflow-y: auto; 
    width: 100%;
    white-space: nowrap; 
    overflow: hidden; 
    text-overflow: ellipsis; 
    min-height: 50px;
  }
  .code-container {
    position: relative;
    display: block;
    margin: 10px 0;
  }
  code {
    display: block; 
    background-color: #f4f4f4;
    padding: 10px;
    border-radius: 4px;
    color: blue;
    width: 100%; 
    box-sizing: border-box; 
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .clipboard-icon {
    position: absolute;
    color: #1DA1F2;
    top: 50%;
    right: 25px;
    transform: translateY(-50%);
    cursor: pointer;
    font-size: 20px; 
  }
  .button-container {
    display: flex;
    justify-content: center;
  }
  button {
    background-color: #1DA1F2;
    color: white;
    border: none;
    border-radius: 20px;
    padding: 10px 20px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  button:hover {
    background-color: #1376b4;
  }
  .intro-text {
    margin: 0 0 40px 0; 
  }
</style>