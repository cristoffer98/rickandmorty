<script>
  export let name;
  export let location;
  export let status;
  export let image;
  export let species;
</script>

<div class="character-card">
  <h2>{name}</h2>
  <img
    src={image}
    alt="Image of {name}"
    on:error={() => (image = "path/to/default/image.jpg")}
  />
  <ul>
    <li>
      <p>Location:</p>
      {location.name}
    </li>
    <li>
      <p>Status:</p>
      {status}
    </li>
    <li>
      <p>Species:</p>
      {species}
    </li>
  </ul>
</div>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");

  * {
    font-family: "Montserrat", sans-serif;
  }
  .character-card {
    margin: 0 auto;
    align-items: center; /* center elements horizontally */
    height: auto; /* set a fixed height */
    padding: 20px; /* add padding */
    border-radius: 10px; /* add rounded corners */
    box-shadow: 2px 2px 4px rgb(7, 7, 7); /* add a drop shadow */
    background-image: url(https://e0.pxfuel.com/wallpapers/395/881/desktop-wallpaper-rick-and-morty-season-2-screencaps-screenshots-and-rick-and-morty-universe.jpg);
  }
  ul {
    padding: 10px;
  }
  li {
    color: rgb(163, 255, 4);
    font-size: 1.2em;
    list-style-type: none;
    display: flex;
  }
  h2 {
    color: rgb(163, 255, 4);
    text-align: center; /* center the text */
    margin-bottom: 10px; /* add margin to bottom of the text */
  }
  p {
    margin-right: 5px;
    color: rgb(13, 203, 255);
  }

  img {
    width: 100%; /* set image width to match card width */
  }
</style>
