<script>
  import Router from "svelte-spa-router";
  import Home from "./pages/Home.svelte";
  import WordMaker from "./pages/WordMaker.svelte";
  import Game from "./pages/Game.svelte";

  const routes = {
    "/": Home,
    "/maker": WordMaker,
  };
</script>

<Router {routes} />
