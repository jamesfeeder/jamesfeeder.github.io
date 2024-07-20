<script lang="ts">
	import { page } from '$app/stores';
	import { targetUrlStore } from './stores';

	/** @type {string} Link to target page.*/
	export let link;
</script>

<a
	href={link}
	on:click={() => {
		targetUrlStore.update((url) => (url = link));
	}}
	class="relative flex h-12 w-12 items-center justify-center rounded-md text-3xl transition-all hover:bg-slate-600 hover:bg-opacity-10 aria-[current=true]:text-blue-600"
	aria-current={$page.url.pathname === link}><slot /></a
>
