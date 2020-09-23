<script>
    import Person from './Person.svelte';
    import StarWarsStore from '../store/StarWars';
    let allPersons = StarWarsStore.getAllPersons();
</script>

<div class="personList">
    {#await allPersons}
        <p class="loader" ></p>
    {:then persons}
        <!-- {JSON.stringify(persons)} -->
        <!-- <p>{JSON.stringify(persons.count)}</p>
        <p>{JSON.stringify(persons.next)}</p>
        <p>{JSON.stringify(persons.previous)}</p>
        <p>{JSON.stringify(persons.results)}</p>
        <p>{JSON.stringify(persons.results[0])}</p> -->
        <!-- <Person person={persons.results[0]} /> -->
        {#each persons.results as person}
        <Person {person}/>
    {/each}
    {:catch error}
        <p>Whoops, there was an error! {JSON.stringify(error)} </p>
    {/await}
</div>

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
  /* border-right: 16px solid green; */
  border-bottom: 16px solid var(--backgroundColor);
  /* border-left: 16px solid pink; */
  width: 120px;
  height: 120px;
  -webkit-animation: spin 2s linear infinite;
  animation: spin 2s linear infinite;
}

@-webkit-keyframes spin {
  0% { -webkit-transform: rotate(0deg); }
  100% { -webkit-transform: rotate(360deg); }
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>