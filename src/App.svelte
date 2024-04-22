<script>
  import Router from "svelte-spa-router";
  import Home from "./pages/Home.svelte";
  import WordMaker from "./pages/WordMaker.svelte";
  import GamePage from "./pages/GamePage.svelte";

  const routes = {
    "/": Home,
    "/maker": WordMaker,
    "/puzzles/:title": GamePage
  };

</script>

<Router {routes} />
