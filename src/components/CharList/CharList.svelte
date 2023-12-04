<script>
  import "./CharList.css";
  import CharListItem from "../CharListItem/CharListItem.svelte";
  import loadingGif from "../../resources/loading.gif";
  import errorGif from "../../resources/error.gif";
  import { takeAllChars } from "../../app/utils";

  export let getCharId;
  let limit = 6;
  let charList = [];
  let loading = true;

  let promiseAll = takeAllChars(limit);

  function newPromise() {
    promiseAll
      .then((value) => {
        charList = [...value];

        loading = false;
      })
      .catch((err) => {
        console.error(err);
      });
  }

  function LoadMore() {
    limit += 6;
    loading = true;
    promiseAll = takeAllChars(limit);
    newPromise();
  }
  newPromise();
</script>

<div class="container char__list p-0">
  <ul class="char__grid row">
    {#each charList as item}
      <a
        on:click={() => getCharId(item.id)}
        class="col-xl-4 col-lg-6 col-md-12 col-6 mb-3"
      >
        <CharListItem
          thumbnailPath={item.thumbnail.path}
          thumbnailExtension={item.thumbnail.extension}
          name={item.name}
        />
      </a>
    {/each}
  </ul>

  {#if loading}
    <div class="loading-gif">
      <img src={loadingGif} alt="loading gif" />
    </div>
  {/if}

  <div class="row">
    <div class="col-12 text-center">
      <button
        class:disabled={loading}
        class="button button__main button__long"
        on:click={() => LoadMore()}
      >
        <div class="inner">load more</div>
      </button>
    </div>
  </div>
</div>

<style>
  .loading-gif {
    width: 100%;
    height: 200px;
  }
  .disabled {
    display: none;
  }
</style>
