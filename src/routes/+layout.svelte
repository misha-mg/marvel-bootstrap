<script>
  import "bootstrap/dist/css/bootstrap.min.css";
  import "./global.css";
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  $: currentRoute = $page.url;

  let navbar;
  onMount(() => {
    navbar = document.querySelector("#navbarNav");
  });

  function toggleNav() {
    navbar.classList.toggle("show");
  }
</script>

<nav class="app__header">
  <div class="container">
    <div class="row">
      <nav class="navbar navbar-expand-md navbar-light">
        <div class="container">
          <h1 class="app__title m-0">
            <a href="/"
              ><strong><span>Marvel</span> information portal</strong></a
            >
          </h1>
          <button
            class="navbar-toggler"
            type="button"
            data-toggle="collapse"
            data-target="#navbarNav"
            aria-controls="navbarNav"
            aria-expanded="false"
            aria-label="Toggle navigation"
            on:click={toggleNav}
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav">
              <li class="nav-item">
                <a class:activeStyle={currentRoute.pathname == "/"} href="/"
                  ><strong>Characters</strong>
                </a>
              </li>
              <p class="d-none d-md-block">/</p>
              <li class="nav-item">
                <a
                  class:activeStyle={currentRoute.pathname == "/comics"}
                  href="/comics"
                >
                  <strong>Comics</strong></a
                >
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </div>
  </div>
</nav>

<slot />

<style>
  .app__title {
    font-size: 28px;
  }
  .navbar-nav {
    font-size: 24px;
  }
  .nav-item {
    margin: 0 8px;
  }
</style>
