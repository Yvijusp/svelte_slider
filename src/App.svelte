<script lang="ts">
  import Slider from './components/Slider.svelte';
  import type { IPost } from './components/interface';

  const fetchPosts = (async (): Promise<IPost[]> => {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');

    return await response.json();
  })();
</script>

<main>
  {#await fetchPosts}
    <p>Loading...</p>
  {:then data}
    <Slider {data} />
  {:catch error}
    <p>An error occured!</p>
  {/await}
</main>

<style>
  main {
    background-color: #f3f3ff;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
