<script>
	import { page } from '$app/stores';

	/** @type {string} Link to target page.*/
	export let link;
</script>

<a
	href={link}
	class="relative flex h-14 w-8 items-center justify-center text-3xl transition-all after:absolute after:bottom-0 after:h-1 after:w-4 after:rounded-full after:bg-transparent after:transition-all hover:after:bg-blue-400 aria-[current=true]:after:w-8 aria-[current=true]:after:bg-blue-600"
	aria-current={$page.url.pathname === link}><slot /></a
>
