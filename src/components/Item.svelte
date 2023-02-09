<script>
  export let name;
  export let image;
  export function setFallbackImage(event) {
    event.target.src = "path/to/default/image.jpg";
  }
</script>

<h3>{name}</h3>
<img
  src={image}
  alt="Image of {name}"
  on:error={() => (image = "path/to/default/image.jpg")}
/>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");

  * {
    font-family: "Montserrat", sans-serif;
  }
  h3 {
    color: aqua;
    text-align: center; /* center the text */
    margin-bottom: 10px; /* add margin to bottom of the text */
  }

  img {
    width: 100%; /* set image width to match card width */
  }
</style>
