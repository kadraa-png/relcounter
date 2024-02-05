<script>
	export let username;
  export let image;
</script>

<div class="container">
  <img src="{image}"/>
  <p>{username}</p>
</div>

<style>
  img {
    max-width: 128px;
    max-height: 128px;
    aspect-ratio: 1;
    border-radius: 50%;
  }

  p {
    font-size: 24pt;
    color: rgb(230, 230, 230);
    padding: 0;
    margin: 0;
    margin-top: 12px;
  }

  .container {
    display: flex;
    align-items: center;
    flex-direction: column;
  }
</style>