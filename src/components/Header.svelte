<style>
  .header {
    display: grid;
    grid-template-columns: 0.1fr 3.9fr;
    height: 100px;
    width: 100%;
    background-color: var(--backgroundColor);
    color: aliceblue;
    margin: 0;
    padding: 10px;
    text-align: center;
    font-family: "Rowdies", cursive;
    margin-bottom: 20px;
  }

  .header > img {
  }

  h1 {
    margin-top: 0;
  }

  h2 {
    margin-bottom: 0;
  }

  h2 > span {
    color: #ffe300;
  }
</style>

<header class="header">
  <img src="/svelte.png" alt="svelte" />
  <div>
    <h1>Star Wars Information</h1>
    <h2>Provided by <span>The Star Wars API</span></h2>
  </div>
</header>
