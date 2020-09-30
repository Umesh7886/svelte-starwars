<script>
  import { fade, fly } from "svelte/transition";
  export let showModal = false;
  export let movie;
  function hide() {
    showModal = false;
  }
</script>

<style>
  .backdrop {
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.9);
    z-index: 99;
  }

  .modal {
    position: relative;
    padding: 10px;
    border-radius: 10px;
    width: 1400px;
    height: 800px;
    margin: 0.1% auto;
    text-align: center;
    background: url("/universe.png");
    background: #000;
    background-size: cover;
    overflow: hidden;
    /* color: #f09f25; */
    color: #ffe300;
  }

  .background-image {
    width: 1400px;
    background: url(/universe.png) 50% 50%;
  }

  .movie-episode {
    text-align: center;
    margin: 40px 0;
  }

  .movie-title {
    text-align: center;
    margin: 0 0 80px 0;
  }

  .crawl {
    font-family: "Krona One", sans-serif;
    text-align: justify;
    margin: 0 auto;
    font-weight: 400;
    font-size: 40px;
    line-height: 70px;
    letter-spacing: 1.1px;
    width: 1000px;
    height: 900px;
    transform: perspective(250px) rotateX(20deg);
    animation: scrollCrawl 20s linear infinite;
    backface-visibility: hidden;
  }

  .crawl:hover {
    -webkit-animation-play-state: paused;
    -moz-animation-play-state: paused;
    -o-animation-play-state: paused;
    animation-play-state: paused;
  }

  .fade-text > span {
    position: absolute;
    top: 20%;
    left: 40%;
    transform: translate(-20%, -40%);
    animation: fadeText 30s linear forwards;
  }

  @keyframes fadeText {
    0% {
      opacity: 0.4;
    }

    15% {
      opacity: 0;
    }

    100% {
      opacity: 0;
    }
  }

  @keyframes scrollCrawl {
    0% {
      transform: perspective(250px) rotateX(20deg) translateY(630px);
      opacity: 1;
    }
    80% {
      opacity: 0.75;
    }

    95% {
      opacity: 0.25;
    }

    100% {
      transform: perspective(250px) rotateX(20deg) translateY(-830px);
      opacity: 0;
    }
  }

  .close {
    cursor: pointer;
    font-size: 64px;
    /* margin-top: -70px; */
    position: absolute;
    right: 10px;
    z-index: 1;
  }

  .close:hover {
    color: #f03939;
    transform: scale(1.5);
  }
</style>

{#if showModal}
  <div class="backdrop" on:click|self>
    <div class="modal background-image " in:fade out:fade>
      <h1 class="fade-text"><span>Hover on crawling text to pause it</span></h1>
      <div class="close" on:click={() => hide()}>&times;</div>
      <div class="crawl">
        <h2 class="movie-title">{movie.title}</h2>
        <h3 class="movie-episode">Episode {movie.episode_id}</h3>
        <p class="">{movie.opening_crawl}</p>
      </div>
    </div>
  </div>
{/if}
