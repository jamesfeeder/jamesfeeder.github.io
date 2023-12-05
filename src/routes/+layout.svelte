<script>
	import { onMount } from 'svelte';
	import { fade, fly, blur } from 'svelte/transition';
	import NavItem from '../lib/NavItem.svelte';
	import NavItemTab from '../lib/NavItemTab.svelte';

	import '../app.css';

	import svelteIcon from '../assets/svelte.svg';
	import { ArrowLeft, ReadCvLogo, Trophy } from 'phosphor-svelte';
	import { beforeNavigate } from '$app/navigation';
	import { targetUrlStore } from '$lib/stores';

	export let data;

	let scrollbarWidth = 0;

	onMount(() => {
		scrollbarWidth = window.innerWidth - document.documentElement.clientWidth;
	});

	/**
	 * Clamp number between two values with the following line.
	 * @param {number} num
	 * @param {number} min
	 * @param {number} max
	 */
	const clamp = (num, min = -1, max = 1) => Math.min(Math.max(num, min), max);

	const pages = ['/', '/achievement', '/cv'];

	let targetUrl = '';
	let transitionDirection = 0;

	targetUrlStore.subscribe((url) => (targetUrl = url));

	beforeNavigate(() => {
		const start = pages.findIndex((e) => e === data.pathname);
		const end = pages.findIndex((e) => e === targetUrl);

		if (start === -1 || end === -1) {
			transitionDirection = 0;
		} else {
			transitionDirection = clamp(end - start);
		}

		// console.log({ startUrl: data.pathname, endUrl: targetUrl, direction: transitionDirection });
	});
</script>

{#if data.pathname !== '/'}
	<nav
		transition:fly={{ y: -60, delay: 240, opacity: 1 }}
		class="fixed left-0 top-0 z-50 border-b border-slate-600 border-opacity-20 bg-slate-50 shadow-sm"
		style={`width: calc(100vw - ${scrollbarWidth}px)`}
	>
		<div
			class="mx-auto flex h-14 max-w-4xl items-center justify-between gap-4 pl-1 pr-3 sm:pl-4 sm:pr-6"
		>
			<div transition:fade={{ duration: 120 }}><NavItem link="/"><ArrowLeft /></NavItem></div>
			<!-- <div class="flex items-center gap-0">
				<NavItemTab link="/achievement"><Trophy /></NavItemTab>
				<NavItemTab link="/cv"><ReadCvLogo /></NavItemTab>
			</div> -->
		</div>
	</nav>
{/if}

{#key data.pathname}
	<div in:fade={{ duration: 120, delay: 120}} out:fade={{ duration: 120}}>
	<div
		in:fly={{
			x: 88 * 0.5 * transitionDirection,
			duration: 240 * Math.abs(transitionDirection),
			delay: 240 * Math.abs(transitionDirection)
		}}
		out:fly={{ x: 88 * 0.5 * -transitionDirection, duration: transitionDirection === 0 ? 120: 240 }}
		class={data.pathname !== '/' ? 'pt-14' : ''}
	>
		<slot />
		<footer class="mx-auto flex h-36 w-full flex-col items-center justify-center gap-2 pt-6 z-50 relative">
			<p class="flex items-center justify-center text-sm">
				Developed with <img class=" h-5 w-5 px-1" src={svelteIcon} alt="svelte logo" /> and ❤️
			</p>
			<a
				class="text-xs text-blue-600 hover:underline hover:underline-offset-2"
				href="https://github.com/jamesfeeder/jamesfeeder.github.io">Source Code</a
			>
		</footer>
	</div>
	</div>
{/key}

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.slate.50);
		color: theme(colors.slate.800);
	}
</style>
