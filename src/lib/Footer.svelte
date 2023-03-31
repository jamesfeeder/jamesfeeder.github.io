<script lang="ts">
  import svelteIcon from "../assets/svelte.svg";
</script>

<footer>
  <p>Developed with <img src={svelteIcon} alt="svelte logo"/> and ❤️</p>
</footer>

<style lang="scss">
  footer {
    // min-height: 240px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 56px 16px;

    p {
      font-size: 0.9rem;

      img {
        margin: 4px 0  -4px;
        width: 18px;
        height: 18px;
        aspect-ratio: 1;
      }
    }
  }
</style>
