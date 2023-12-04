<script>
  import { takeOneChar } from "../app/utils";
  import CharInfo from "../components/CharInfo/CharInfo.svelte";
  import CharList from "../components/CharList/CharList.svelte";
  import RandomChar from "../components/RandomChar/RandomChar.svelte";

  let id = Math.floor(Math.random() * 400 + 1011000);
  let idFromList;
  let limit = 9;

  function getCharId(newId) {
    idFromList = newId;
    promiseOne = takeOneChar(newId);
  }

  let promiseOne = takeOneChar(id);
</script>

<RandomChar />

<div class="container list-char-container">
  <div class="row char__list-row d-flex justify-content-between">
    <div class="col-xl-8 col-md-6">
      <CharList {getCharId} />
    </div>
    <div class="col-xl-4 col-md-6 char__info-container mb-5">
      <CharInfo {promiseOne} />
    </div>
  </div>
</div>

<style>
  .list-char-container {
    padding: 0;
  }
</style>
