<script>
	import { fade, fly, blur } from 'svelte/transition';
	import NavItem from '../lib/NavItem.svelte';
	import NavItemTab from '../lib/NavItemTab.svelte';
	import Anchor from '$lib/Anchor.svelte';

	import '../app.css';

	import svelteIcon from '../assets/svelte.svg';
	import { ArrowLeft, ReadCvLogo, Trophy } from 'phosphor-svelte';
	import { beforeNavigate } from '$app/navigation';
	import { targetUrlStore } from '$lib/stores';

	export let data;

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

		console.log({ startUrl: data.pathname, endUrl: targetUrl, direction: transitionDirection });
	});
</script>

{#if data.pathname !== '/'}
	<nav
		transition:fly={{ y: -60, delay: 240, opacity: 1 }}
		class="fixed z-50 w-full border-b border-slate-600 border-opacity-20 bg-slate-50 shadow-sm"
	>
		<div class="mx-auto flex h-14 max-w-4xl items-center justify-between gap-4 px-4 sm:px-6">
			<div transition:fade={{ duration: 120 }}><NavItem link="/"><ArrowLeft /></NavItem></div>
			<div class="flex items-center gap-0 px-4 sm:px-6">
				<NavItemTab link="/achievement"><Trophy /></NavItemTab>
				<NavItemTab link="/cv"><ReadCvLogo /></NavItemTab>
			</div>
		</div>
	</nav>
{/if}

{#key data.pathname}
	<div in:blur={{ duration: 240, delay: 240, amount: 4 }} out:blur={{ duration: 120, amount: 8 }}>
		<div
			in:fly={{
				x: 88 * transitionDirection,
				duration: 160 * Math.abs(transitionDirection),
				delay: 240 * Math.abs(transitionDirection)
			}}
			out:fly={{ x: 88 * -transitionDirection, duration: transitionDirection === 0 ? 120 : 240 }}
			class={data.pathname !== '/' ? 'pt-14' : ''}
		>
			<slot />
			<footer class="mx-auto flex h-36 w-full flex-col items-center justify-center gap-2 pt-6">
				<p class="flex items-center justify-center text-sm">
					Developed with <img class=" h-5 w-5 px-1" src={svelteIcon} alt="svelte logo" /> and ❤️
				</p>
				<Anchor
					additionalClass="text-xs border-b"
					label="Source Code"
					link="https://github.com/jamesfeeder/jamesfeeder.github.io"
					openNewTab
				/>
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
