<script>
  import Item from "./Item.svelte";
  import CharacterInfo from "./CharacterInfo.svelte";
  import PrevNextButton from "./buttons/PrevNextButton.svelte";

  let characters;
  let showList = true;
  let lastPage;
  let selectedCharacter;
  let filteredCharacters = [];
  let filteredCharactersValid = false;
  let firstTimeSearch = false;
  let search = "";
  let loading = false;
  let searching = false;
  let inputValid = false;
  let inputText = "";
  let currentPage = 1;

  async function getData(search, pageNumber) {
    loading = true;
    if (search) {
      try {
        const response = await fetch(
          `https://rickandmortyapi.com/api/character/?name=${search}&page=${pageNumber}`
        );
        if (!response.ok) {
          if (response.status === 404) {
            updateFilteredCharacters([]);
          }
          throw new Error(response.statusText);
        }
        const data = await response.json();
        lastPage = data.info.pages;
        characters = data.results;
        updateFilteredCharacters(
          characters.filter((character) =>
            character.name.toLowerCase().includes(search.toLowerCase())
          )
        );
        loading = false;
      } catch (error) {
        console.error(error);
      }
    }
  }
  getData();

  function updateFilteredCharacters(newCharacters) {
    filteredCharacters = newCharacters;
    filteredCharactersValid = filteredCharacters.length !== 0;
  }

  function validateSearch() {
    if (search.trim()) {
      filterData();
    }
  }

  function filterData() {
    firstTimeSearch = true;
    searching = true;
    getData(search.trim());
    searching = false;
    inputText = search;
  }

  function showCharacter(character) {
    selectedCharacter = character;
    showList = false;
  }
  function returnToList() {
    selectedCharacter = null;
    showList = true;
  }
  function loadPage(pageNumber) {
    currentPage = pageNumber;
    getData(search, currentPage);
  }
</script>

<div class="character-list-container">
  {#if !showList}
    <button class="return-button" on:click={returnToList}>Return</button>
  {:else}
    <form on:submit|preventDefault={validateSearch}>
      <input
        type="text"
        bind:value={search}
        on:input={() => (inputValid = search.trim().length > 0)}
        placeholder="Search for a character"
      />
      <button class="submit-button" type="submit" disabled={!inputValid}
        >Search</button
      >
    </form>
  {/if}
  {#if searching}
    <p>Loading...</p>
  {:else if filteredCharacters.length}
    <div class="prevNextBtn" class:hidden={!showList}>
      <PrevNextButton {currentPage} {lastPage} {loadPage} />
    </div>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <ul class:hidden={!showList}>
      {#each filteredCharacters as character}
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <li on:click={() => showCharacter(character)}>
          <Item {...character} />
        </li>
      {/each}
    </ul>
    <div class="prevNextBtn" class:hidden={!showList}>
      <PrevNextButton {currentPage} {lastPage} {loadPage} />
    </div>
  {:else if filteredCharacters.length === 0 && firstTimeSearch === true}
    <p>No characters found for {inputText}</p>
  {/if}
  {#if selectedCharacter}
    <CharacterInfo {...selectedCharacter} />
  {/if}
</div>

<style>
  .prevNextBtn {
    margin: 10px 0 10px 0;
  }
  .hidden {
    display: none;
  }
  .character-list-container {
    margin: 0 auto;
    margin-bottom: 40px;
  }
  ul {
    display: flex;
    flex-wrap: wrap; /* wrap items to the next row */
    justify-content: center; /* distribute items evenly horizontally */
    margin: 0 auto;
    padding: 0;
  }
  li {
    list-style-type: none;
    display: flex;
    flex-direction: column; /* stack elements vertically */
    align-items: center; /* center elements horizontally */
    width: 300px; /* set a fixed width */
    height: 400px; /* set a fixed height */
    margin: 10px; /* add margin */
    padding: 20px; /* add padding */
    border-radius: 10px; /* add rounded corners */
    box-shadow: 2px 2px 4px rgb(7, 7, 7); /* add a drop shadow */
    background-image: url(https://e0.pxfuel.com/wallpapers/395/881/desktop-wallpaper-rick-and-morty-season-2-screencaps-screenshots-and-rick-and-morty-universe.jpg);
  }
  li:hover {
    cursor: pointer;
    scale: 1.05;
    transition: 0.3s;
  }
  form {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  input {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 5px 0 0 5px;
  }
  .submit-button {
    display: inline-block;
    outline: none;
    cursor: pointer;
    background-color: #0070d2;
    border-radius: 0 5px 5px 0;
    border: 1px solid #0070d2;
    color: #fff;
    font-weight: 400;
    text-align: center;
  }
  .submit-button:hover {
    background-color: #005fb2;
    border-color: #005fb2;
  }

  .return-button {
    padding: 0.5rem 1rem;
    background-color: rgb(0, 195, 255);
    color: white;
    border: none;
    border-radius: 5px;
    font-weight: bold;
    cursor: pointer;
    margin-bottom: 20px;
  }
  .return-button:hover {
    background-color: rgb(2, 255, 53);
  }
</style>
