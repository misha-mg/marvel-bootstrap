<script>
  import "./RandomChar.css";
  import RandomCharInfo from "../RandomCharInfo/RandomCharInfo.svelte";
  import RandomCharStatic from "../RandomCharStatic/RandomCharStatic.svelte";
  import { takeOneChar } from "../../app/utils";

  let id = Math.floor(Math.random() * 400 + 1011000);
  let promise = takeOneChar(id);
  function updateChar() {
    id = Math.floor(Math.random() * 400 + 1011000);
    promise = takeOneChar(id);
  }
</script>

<div class="container randomchar">
  <div class="row mb-lg-5 mb-3">
    <RandomCharInfo {promise} />
    <RandomCharStatic {updateChar} />
  </div>
</div>
<!-- <div class="randomchar"></div> -->
