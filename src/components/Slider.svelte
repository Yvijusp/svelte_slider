<script lang="ts">
  import { leftArrow, rightArrow } from '../assets/icon';
  import Card from './Card.svelte';
  import type { IPost } from './interface';
  export let data: IPost[];

  let perPage = 2;
  let currentPage = 1;
  let totalPages = 3;

  $: indexOfLastPage = currentPage * perPage;
  $: indexOfFirstPage = indexOfLastPage - perPage;

  $: currentData = data.slice(indexOfFirstPage, indexOfLastPage);

  const nextPage = () => {
    if (currentPage < totalPages) {
      return currentPage++;
    }
    return;
  };

  const lastPage = () => {
    if (currentPage > 1) {
      return currentPage--;
    }
    return;
  };
</script>

<div class="container">
  <h2>Posts slider</h2>
  <div class="slider">
    <button class="arrow right-arrow" on:click={lastPage}
      >{@html rightArrow}</button
    >
    {#each currentData as post (post.id)}
      <Card {post} />
    {/each}
    <button class="arrow left-arrow" on:click={nextPage}
      >{@html leftArrow}</button
    >
  </div>
  <div class="slider-page">
    {#each Array(totalPages).fill(null) as circle, index}
      {#if currentPage === index + 1}
        <span class="circle"><span class="circle-active" /></span>
      {:else}
        <span class="circle" />
      {/if}
    {/each}
  </div>
</div>

<style>
  .container {
    width: 1280px;
    margin: 0 auto;
  }

  h2 {
    text-align: center;
  }

  .slider {
    position: relative;
    width: 100%;
    padding: 30px;
    display: flex;
    gap: 20px;
    align-items: center;
    justify-content: center;
  }

  .arrow {
    background-color: #fff;
    border: 1px solid #c4cafb;
    opacity: 0.5;
    width: 66px;
    height: 66px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 100%;
    cursor: pointer;
  }

  .right-arrow {
    position: absolute;
    left: 0;
    top: 40%;
  }

  .left-arrow {
    position: absolute;
    right: 0;
    top: 40%;
  }

  .slider-page {
    width: 100%;
    display: flex;
    justify-content: center;
    gap: 5px;
  }

  .circle {
    border-radius: 100%;
    height: 18px;
    width: 18px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #d5ddf7;
  }

  .circle-active {
    border-radius: 100%;
    height: 10px;
    width: 10px;

    background-color: #fff;
  }
</style>
