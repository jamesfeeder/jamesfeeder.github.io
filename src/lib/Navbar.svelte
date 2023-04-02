<script lang="ts">
  import { fly } from "svelte/transition";
  import { quartInOut } from "svelte/easing";
  import { link, location } from "svelte-spa-router";
  import active from "svelte-spa-router/active";
  import BackIcon from "../assets/BackIcon.svelte";
</script>

{#if $location !== "/"}
  <nav transition:fly={{ duration: 240, y: -56, easing: quartInOut }}>
    <div>
      <ul>
        <li>
          <a href="/" use:link use:active><BackIcon />Back</a>
        </li>
        <!-- <li><a href="/resume" use:link use:active>Résumé</a></li> -->
      </ul>
      <div />
    </div>
  </nav>
{/if}

<style lang="scss">
  nav {
    position: fixed;
    top: 0;
    width: 100%;
    height: 56px;
  }

  div {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 800px;
    padding: 0 16px;
    height: 100%;
    margin: auto;
  }

  ul {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0;
    padding: 0;
    list-style-type: none;

    li {
      a {
        padding: 4px 8px;
        margin-left: -8px; // 8px
        font-weight: 600;
      }
    }
  }

  :global(a.active) {
    font-weight: 800;
  }
</style>
