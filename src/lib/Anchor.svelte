<script>
	import { ArrowSquareOut, ArrowRight } from 'phosphor-svelte';
	import { targetUrlStore } from './stores';

	/**  @type {string} Anchor Label*/
	export let label;
	/**  @type {string} Link to Open*/
	export let link;
	/**  @type {boolean} Open in new tab?*/
	export let openNewTab = false;
	/** @type {string} Additional Class*/
	export let additionalClass = '';
	/**  @type {boolean} Disable icon*/
	export let disableIcon = false;
</script>

<a
	href={link}
	target={openNewTab ? '_blank' : undefined}
	on:click={() => {
		targetUrlStore.update((url) => (url = link));
	}}
	class={`group relative flex items-center gap-1 border-b-2 border-transparent font-medium text-blue-600 transition hover:z-10 hover:border-current hover:bg-slate-50   ${additionalClass}`}
	>{label}

	{#if !disableIcon}
		<div
			class={`absolute right-0 top-0 isolate -z-10 box-content flex h-full translate-x-0 items-center justify-center border-b-2 border-current pl-1 text-transparent transition-all group-hover:translate-x-full group-hover:bg-slate-50 group-hover:text-inherit  ${additionalClass}`}
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
