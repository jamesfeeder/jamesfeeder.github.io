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
	class="group relative isolate flex translate-x-0 items-center justify-center gap-1 rounded-full bg-inherit font-medium text-slate-600 underline decoration-slate-600 underline-offset-8 transition duration-300 hover:-translate-x-3 hover:bg-slate-600 hover:text-white hover:no-underline hover:decoration-slate-600 hover:duration-75 active:scale-95 dark:text-slate-400 dark:decoration-slate-400"
>
	<div
		class="relative left-0 z-10 flex items-center justify-center gap-1 rounded-full bg-inherit px-2.5 py-1"
	>
		{label}
	</div>
	{#if !disableIcon}
		<div
			class="absolute right-0 top-0 z-0 flex h-full translate-x-0 items-center rounded-full bg-slate-600 pl-6 pr-2 text-white opacity-0 transition group-hover:translate-x-6 group-hover:opacity-100 group-hover:duration-150"
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
