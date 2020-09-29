<script>
  import StarWarsStore from "../store/StarWars";
  import Modal from "./Modal.svelte";

  export let person = {};
  let HomeWorldInfo = StarWarsStore.getByURL(person.homeworld);
  let MovieInfo = StarWarsStore.getMovies(person.films);

  let showModal = false;
  let selectedEpisode = 0;
  let enableBlur = false;
  let toggleModal = ({ target }) => {
    selectedEpisode = target.dataset.episodeid;
    showModal = !showModal;
    enableBlur = !enableBlur;
  };
</script>

<style>
  .person {
    background: linear-gradient(#dce4f5, #c3ddff);
    box-shadow: 2px 2px 3px #9dc5f4;
    margin: 10px;
    width: 300px;
    text-align: center;
    border-radius: 10px;
    line-height: 1.5;
  }
  .stat p {
    margin: 4px;
  }

  .scroll {
    cursor: pointer;
    background: linear-gradient(#c3ddff, #dce4f5);
    height: 40px;
    padding: 10px 5px;
    transition: all 0.2s linear;
    color: #2b2929;
  }

  .scroll:hover {
    background: #70a8f1;
    color: #fff;
  }

  .name {
    background: #1b6ce6;
    color: #fff;
    width: 100%;
    padding: 10px 5px;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    font-weight: 500;
  }
</style>

<div class="person">
  <div class="name">
    <h2>{person.name}</h2>
  </div>
  <div class="stat">
    <p>Birth Year: {person.birth_year}</p>
    <p>Height: {person.height}</p>
    <p>Mass: {person.height}</p>
    {#await HomeWorldInfo}
      <p>Homeworld: ....</p>
    {:then homeworld}
      <p>HomeWorld: {homeworld.name}</p>
      <p>HomeWorld Population: {homeworld.population}</p>
    {:catch error}
      <p>Whoops, there was an error! {JSON.stringify(error)}</p>
    {/await}

    {#await MovieInfo}
      <h3>Loading....</h3>
    {:then movies}
      {#each movies as movie}
        <div class="scroll">
          <p on:click={toggleModal} data-episodeid={movie.episode_id}>
            {movie.title}
          </p>
          {#if selectedEpisode == movie.episode_id}
            <Modal {showModal} {movie} on:click={toggleModal} />
          {/if}
        </div>
      {/each}
    {:catch error}
      <p>Whoops</p>
    {/await}
  </div>
</div>
