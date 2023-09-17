<script>
	/**  @type {string} Anchor Label*/
	export let label;
	/**  @type {string} Link to Open*/
	export let link;
	/**  @type {boolean} Open in new tab?*/
	export let openNewTab = false;
	import { ArrowSquareOut, ArrowRight } from 'phosphor-svelte';
</script>

<a
	href={link}
	target={openNewTab ? '_blank' : '_self'}
	class="group relative isolate flex items-center gap-1 border-b-2 border-transparent font-medium text-blue-600 transition-all hover:z-10 hover:border-current hover:bg-white active:z-10 active:border-current active:bg-white"
	>{label}
	<div
		class="absolute right-0 top-0 isolate -z-10 box-content flex h-full translate-x-4 items-center justify-center border-b-2 border-current pl-2 pr-1 opacity-0 transition-all group-hover:translate-x-6 group-hover:bg-white group-hover:opacity-100 group-active:translate-x-6 group-active:bg-white group-active:opacity-100"
	>
		<slot
			>{#if openNewTab}
				<ArrowSquareOut weight="bold" />
			{:else}
				<ArrowRight weight="bold" />
			{/if}</slot
		>
	</div>
</a>
