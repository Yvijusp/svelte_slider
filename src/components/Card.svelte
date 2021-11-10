<script lang="ts">
  import type { IPost } from './interface';

  export let post: IPost;
</script>

<div class="card">
  <h2>{post.title}</h2>
  <p>{post.body}</p>
</div>

<style>
  .card {
    width: 450px;
    height: 280px;
    padding: 40px;

    background-color: #fff;

    box-shadow: 0 25px 25px -20px rgba(1, 42, 154, 0.16);
    border-radius: 20px;
  }

  h2 {
    margin-bottom: 7px;
  }
</style>
