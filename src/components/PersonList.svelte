<script>
  import Person from "./Person.svelte";
  import StarWarsStore from "../store/StarWars";
  let allPersons = StarWarsStore.getAllPersons();
  function loadList({ target }) {
    if (target.dataset.link != null) {
      allPersons = StarWarsStore.getByURL(target.dataset.link);
    }
  }
</script>

<style>
  .personList {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .loader {
    border: 16px solid #f3f3f3;
    border-radius: 50%;
    border-top: 16px solid var(--backgroundColor);
    border-bottom: 16px solid var(--backgroundColor);
    width: 120px;
    height: 120px;
    -webkit-animation: spin 1s linear infinite;
    animation: spin 1s linear infinite;
  }

  @-webkit-keyframes spin {
    0% {
      -webkit-transform: rotate(0deg);
    }
    100% {
      -webkit-transform: rotate(360deg);
    }
  }

  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  .buttons {
    width: 100%;
    text-align: center;
  }

  #left,
  #right {
    margin-left: 50px;
    margin-top: 20px;
    display: inline-block;
    width: 200px;
    height: 40px;
    position: relative;
    background: #1b6ce3;
    cursor: pointer;
    color: #fff;
    outline: none;
    border: none;
  }

  #left:hover::after {
    content: "";
    position: absolute;
    right: 0;
    bottom: 0;
    width: 0;
    height: 0;
    border-right: 20px solid white;
    border-top: 20px solid transparent;
    border-bottom: 20px solid transparent;
  }

  #right:hover::after {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0;
    width: 0;
    height: 0;
    border-left: 20px solid white;
    border-top: 20px solid transparent;
    border-bottom: 20px solid transparent;
  }

  #left:hover::before {
    content: "";
    position: absolute;
    left: -20px;
    bottom: 0;
    width: 0;
    height: 0;
    border-right: 20px solid #1b6ce6;
    border-top: 20px solid transparent;
    border-bottom: 20px solid transparent;
  }

  #right:hover::before {
    content: "";
    position: absolute;
    right: -20px;
    bottom: 0;
    width: 0;
    height: 0;
    border-left: 20px solid #1b6ce6;
    border-top: 20px solid transparent;
    border-bottom: 20px solid transparent;
  }

  span {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    color: white;
    cursor: pointer;
  }

  #right:disabled,
  #left:disabled {
    background-color: #f3ef08;
    color: #1b6ce6;
    cursor: not-allowed;
    /* pointer-events: none; */
  }
</style>

<div class="personList">
  {#await allPersons}
    <p class="loader" />
  {:then persons}
    {#each persons.results as person}
      <Person {person} />
    {/each}
    <div class="buttons">
      <button
        id="left"
        data-link={persons.previous}
        disabled={persons.previous ? '' : 'true'}
        on:click={loadList}>{persons.previous ? 'Prev 10' : 'No previous to show'}</button>
      <button
        id="right"
        data-link={persons.next}
        disabled={persons.next ? '' : 'true'}
        on:click={loadList}>{persons.next ? 'Next 10' : 'Nothing more to show'}</button>
    </div>
  {:catch error}
    <p>Whoops, there was an error! {JSON.stringify(error)}</p>
  {/await}
</div>
