<script>
	import { Svrollbar } from 'svrollbar';
	import svelteIcon from '../assets/svelte.svg';
	import '../app.css';
</script>

<Svrollbar />
<slot />
<footer class="mx-auto flex h-36 w-full items-center justify-center pt-6">
	<p class="flex items-center justify-center">
		Developed with <img class=" h-6 w-6 px-1" src={svelteIcon} alt="svelte logo" /> and ❤️
	</p>
</footer>

<style lang="postcss">
	:global(html) {
		color: theme(colors.slate.800);
		-ms-overflow-style: none; /* IE and Edge */
		scrollbar-width: none; /* Firefox */
	}

	:global(html::-webkit-scrollbar) {
		display: none;
	}
</style>
