<script>
  import "./ComicsList.css";
  import loadingGif from "../../resources/loading.gif";
  import errorGif from "../../resources/error.gif";
  import { takeAllComics } from "../../app/utils";
  import ComicsListItem from "../ComicsListItem/ComicsListItem.svelte";
  import { setContext } from "svelte";

  let offset = 210;
  let comicsList = [];
  let loading = true;
  export let getComicId = () => {};
  let comicId = 4;

  let promiseAll = takeAllComics(offset);

  function newPromise() {
    promiseAll
      .then((value) => {
        comicsList = [...comicsList, ...value];
        loading = false;
      })
      .catch((err) => {
        console.error(err);
      });
  }

  function LoadMore() {
    offset += 8;
    loading = true;
    promiseAll = takeAllComics(offset);
    newPromise();
  }
  newPromise();
</script>

<div class="container comics__list">
  <div class="row">
    {#each comicsList as comic}
      <div class="col-md-3 col-sm-4 col-6 mb-md-4 mb-3">
        <a on:click={() => getComicId(comic.id)} href="/comics/{comic.id}">
          <ComicsListItem
            path={comic.thumbnail.path}
            extension={comic.thumbnail.extension}
            name={comic.name}
            title={comic.title}
            price={comic.prices[0].price}
          />
        </a>
      </div>
    {/each}
  </div>
  <div class="row">
    <div class="col-12">
      {#if loading}
        <div class="loading-gif-block">
          <img src={loadingGif} alt="loading gif" />
        </div>
      {/if}
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
