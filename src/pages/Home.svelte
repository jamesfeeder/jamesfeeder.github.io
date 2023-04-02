<script lang="ts">
  import { link } from "svelte-spa-router";
  import { fly, blur } from "svelte/transition";
  import { quartInOut } from "svelte/easing";
  import { scrollRef } from "../utils/stores";
  import { onDestroy } from "svelte";

  let scrollRefValue: Element;

  scrollRef.subscribe((value) => {
    scrollRefValue = value;
  });

  onDestroy(() => {
    scrollRefValue.scrollTop = 0;
  });
</script>

<main
  in:fly={{ x: -120, duration: 480, easing: quartInOut }}
  out:fly={{ y: -120, duration: 240, easing: quartInOut }}
>
  <header in:blur={{ duration: 600 }} out:blur={{ duration: 200 }}>
    <h1>Jetsadakorn Maliwan</h1>
    <div class="subtitle">
      <h4>Software Developer /</h4>
      <h4>Front-End Web Developer</h4>
    </div>
    <div class="button-bar">
      <a class="button" href="https://github.com/jamesfeeder" target="_blank">
        Github Profile
      </a>
      <a class="button clear" href="#/resume" use:link> Résumé </a>
    </div>
  </header>
</main>

<style lang="scss">
  main {
    max-width: 800px;
    padding: 16px;
    margin: auto;

    header {
      height: calc(100dvh - (56px + (16px * 2)));
      display: flex;
      flex-direction: column;
      justify-content: center;

      h1 {
        font-size: 2.6rem;
        margin-top: 0;
        margin-bottom: 8px;
      }

      .subtitle {
        display: flex;
        flex-wrap: wrap;
        column-gap: 6px;
        margin-top: 8px;
        margin-bottom: 24px;

        h4 {
          color: hsl(0, 0%, 50%);
          margin: 0;
        }
      }

      .button-bar {
        display: flex;
        flex-wrap: wrap;
        gap: 16px;
        margin-bottom: 88px;
      }
    }
  }
</style>
