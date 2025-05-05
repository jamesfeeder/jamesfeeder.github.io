<script lang="ts">
	import { onMount } from 'svelte';
	import { fade, fly, blur } from 'svelte/transition';
	import NavItem from '../lib/NavItem.svelte';
	import NavItemTab from '../lib/NavItemTab.svelte';

	import '../app.css';

	import svelteIcon from '../assets/svelte.svg';
	import { ArrowLeft, At, CaretLeft, Info, ReadCvLogo, Trophy } from 'phosphor-svelte';
	import { beforeNavigate } from '$app/navigation';
	import { targetUrlStore } from '$lib/stores';

	let { data, children } = $props();

	let scrollbarWidth = $state(0);

	onMount(() => {
		scrollbarWidth = window.innerWidth - document.documentElement.clientWidth;
	});

	const clamp = (num: number, min = -1, max = 1) => Math.min(Math.max(num, min), max);

	const pages = ['/', '/achievement', '/cv'];

	let targetUrl = '';
	let transitionDirection = $state(0);

	targetUrlStore.subscribe((url) => (targetUrl = url));

	beforeNavigate(() => {
		const start = pages.findIndex((e) => e === data.pathname);
		const end = pages.findIndex((e) => e === targetUrl);

		if (start === -1 || end === -1) {
			transitionDirection = 0;
		} else {
			transitionDirection = clamp(end - start);
		}
	});
</script>

{#if data.pathname !== '/'}
	<nav
		transition:fly={{ y: -60, delay: 120, opacity: 1, duration: 500 }}
		class="fixed left-0 top-0 z-50 border-b border-slate-200 border-opacity-20 bg-slate-50 shadow-2xl shadow-slate-200 dark:border-slate-900 dark:bg-slate-900 dark:shadow-slate-950"
		style={`width: calc(100vw - ${scrollbarWidth}px)`}
	>
		<div
			class="mx-auto flex h-14 max-w-4xl items-center justify-between gap-4 pl-1 pr-1 sm:pl-4 sm:pr-4"
		>
			<div>
				{#if data.pathname !== '/'}
					<div transition:fade={{ duration: 120 }}><NavItem link="/"><CaretLeft /></NavItem></div>
				{/if}
			</div>
			<!-- <div class="flex items-center gap-0">
				<NavItem link="/cv"><Info /></NavItem>
			</div> -->
		</div>
	</nav>
{/if}

{#key data.pathname}
	<div in:fade={{ duration: 120, delay: 120 }} out:fade={{ duration: 120 }}>
		<div
			in:fly={{
				x: 88 * 0.5 * transitionDirection,
				duration: 240 * Math.abs(transitionDirection),
				delay: 240 * Math.abs(transitionDirection)
			}}
			out:fly={{
				x: 88 * 0.5 * -transitionDirection,
				duration: transitionDirection === 0 ? 120 : 240
			}}
			class={data.pathname !== '/' ? 'pt-14' : ''}
		>
			{@render children?.()}
			<footer
				class="relative z-50 mx-auto flex h-36 w-full flex-col items-center justify-center gap-2 pt-6"
			>
				<p class="flex items-center justify-center text-sm">
					Developed with <img class=" h-5 w-5 px-1" src={svelteIcon} alt="svelte logo" /> and ❤️
				</p>
				<a
					class="text-xs  hover:underline hover:underline-offset-2"
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

		@media (prefers-color-scheme: dark) {
			background-color: theme(colors.slate.900);
			color: theme(colors.slate.200);
		}
	}

	:global(a) {
		color: theme(colors.blue.600);

		@media (prefers-color-scheme: dark) {
			color: theme(colors.blue.400);
		}
	}
</style>
