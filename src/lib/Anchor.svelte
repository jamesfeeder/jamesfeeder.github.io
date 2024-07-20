<script>
	import { ArrowSquareOut, ArrowRight } from 'phosphor-svelte';
	import { targetUrlStore } from './stores';

	/**  @type {string} Anchor Label*/
	export let label;
	/**  @type {string} Link to Open*/
	export let link;
	/**  @type {boolean} Open in new tab?*/
	export let openNewTab = false;
	/**  @type {boolean} Disable icon*/
	export let disableIcon = false;
</script>

<a
	href={link}
	target={openNewTab ? '_blank' : undefined}
	on:click={() => {
		targetUrlStore.update((url) => (url = link));
	}}
	class="group relative flex items-center justify-center gap-1 rounded-full bg-inherit px-2.5 py-1 font-medium text-blue-600 transition duration-300 hover:z-10 hover:border-current hover:bg-blue-600 hover:text-white hover:duration-75 active:scale-95"
	>{label}

	{#if !disableIcon}
		<div
			class="absolute right-0 top-0 isolate -z-10 flex h-full translate-x-0 items-center rounded-full bg-blue-600 pl-6 pr-2 text-white opacity-0 transition group-hover:translate-x-[40%] group-hover:opacity-100 group-hover:duration-150"
		>
			<slot
				>{#if openNewTab}
					<ArrowSquareOut weight="bold" />
				{:else}
					<ArrowRight weight="bold" />
				{/if}</slot
			>
		</div>
	{/if}
</a>
