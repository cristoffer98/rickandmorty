<script>
  export let currentPage;
  export let lastPage;
  export let loadPage;
</script>

<div class="prev-next-container">
  <button
    class="left-btn"
    on:click={() => loadPage(currentPage - 1)}
    disabled={currentPage === 1}
    ><i class="fas fa-arrow-left" />
  </button>
  <h3>{currentPage}</h3>
  <button
    class="right-btn"
    on:click={() => loadPage(currentPage + 1)}
    disabled={currentPage === lastPage}><i class="fas fa-arrow-right" /></button
  >
</div>

<style>
  button {
    border: none;
    padding: 0 30px 0 30px;
  }
  button:hover {
    background-color: rgb(103, 161, 3);
  }
  .left-btn {
    border-radius: 10px 0 0 10px;
    background: #a3ff04;
    background: linear-gradient(
      90deg,
      rgba(163, 255, 4, 1) 22%,
      rgba(0, 255, 255, 1) 100%
    );
  }
  .left-btn:hover {
    background: rgb(100, 158, 0);
    background: linear-gradient(90deg, #649e00 22%, rgba(0, 255, 255, 1) 100%);
  }
  .right-btn {
    border-radius: 0 10px 10px 0;
    background: rgb(0, 255, 255);
    background: linear-gradient(
      90deg,
      rgba(0, 255, 255, 1) 22%,
      rgba(163, 255, 4, 1) 100%
    );
  }
  .right-btn:hover {
    background: rgb(0, 255, 255);
    background: linear-gradient(
      90deg,
      rgba(0, 255, 255, 1) 22%,
      rgba(100, 158, 0, 1) 100%
    );
  }
  h3 {
    padding: 10px 20px 10px 20px;
    margin: 0;
    background: aqua;
  }
  .prev-next-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
</style>
