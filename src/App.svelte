<script lang="ts">
  import "overlayscrollbars/overlayscrollbars.css";

  import { afterUpdate } from "svelte";
  import Router from "svelte-spa-router";
  import { OverlayScrollbarsComponent } from "overlayscrollbars-svelte";
  import Cursor from "./lib/Cursor.svelte";
  import Navbar from "./lib/Navbar.svelte";
  import Home from "./pages/Home.svelte";
  import Resume from "./pages/Resume.svelte";
  import Footer from "./lib/Footer.svelte";

  let cursor;

  afterUpdate(() => {
    cursor.updateIntractableElements();
  });

  const routes = {
    // Exact path
    "/": Home,
    "/resume": Resume,

    // Using named parameters, with last being optional
    // '/author/:first/:last?': Author,

    // Wildcard parameter
    // '/book/*': Book,

    // Catch-all
    // This is optional, but if present it must be the last
    // '*': NotFound,
  };
</script>

<OverlayScrollbarsComponent
  style="height: 100dvh; width: 100dvw"
  element="span"
  options={{ scrollbars: { autoHide: "scroll" } }}
>
  <Cursor bind:this={cursor} />
  <Navbar />
  <div class="content">
    <Router
      {routes}
      on:routeLoaded={async () => {
        cursor.updateIntractableElements();
      }}
    />
  </div>
  <Footer />
</OverlayScrollbarsComponent>

<style lang="scss">
  .content {
    // display: flex;
    margin-top: calc(56px);
  }
</style>
