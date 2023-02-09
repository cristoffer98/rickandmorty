<script>
  import Characters from "./components/Characters.svelte";

  function reloadPage() {
    location.reload();
  }
</script>

<div class="main-layer-container">
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <img
    on:click={reloadPage}
    src="https://logos-world.net/wp-content/uploads/2022/01/Rick-And-Morty-Logo.png"
    alt="rick and morty logo"
  />
  <Characters />
</div>

<style>
  .main-layer-container {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }
  img {
    width: 20rem;
  }
  img:hover {
    cursor: pointer;
  }

  @media (min-width: 640px) {
    .main-layer-container {
      max-width: none;
    }
    img {
      width: 20rem;
    }
  }
</style>
