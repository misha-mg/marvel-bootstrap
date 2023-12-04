<script>
  import "./SingleComicPage.css";
  import AppBanner from "../../components/AppBanner/AppBanner.svelte";
  import loadingGif from "../../resources/loading.gif";
  import errorGif from "../../resources/error.gif";
  import { getOneComic } from "../../app/utils.js";

  export let comicId;

  let promiseOne = getOneComic(comicId);
</script>

<AppBanner />

<div class="container single-comic-container p-0">
  <div class="row">
    {#await promiseOne}
      <div class="loading-gif-block">
        <img src={loadingGif} alt="loading gif" />
      </div>
    {:then response}
      <div class="col-md-3 col-sm-5 mb-sm-0 mb-3">
        <img
          src={`${response[0].thumbnail.path}.${response[0].thumbnail.extension}`}
          alt="name"
          class="single-comic__img"
        />
      </div>
      <div class="col-md-7 col-sm-7">
        <h3 class="single-comic__title">
          {response[0].title}
        </h3>
        <p class="single-comic__description">
          {response[0].description
            ? response[0].description
            : "There is no description"}
        </p>
        <p class="single-comic__description">
          Pages: {response[0].pageCount}
        </p>
        <p class="single-comic__description">Language: en-us</p>
        <div class="single-comic__price">{response[0].prices[0].price}</div>
      </div>
      <div
        class="col-md-2 col-sm-12 order-md-last order-first mb-3 mb-md-0 text-end"
      >
        <a href="../comics" class="single-comic__back">Back to all</a>
      </div>
    {:catch error}
      <img src={errorGif} alt="errorGif" />
    {/await}
  </div>
</div>
