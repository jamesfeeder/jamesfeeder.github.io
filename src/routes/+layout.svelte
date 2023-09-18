<script>
	import NavItem from './NavItem.svelte';

	import svelteIcon from '../assets/svelte.svg';
	import '../app.css';
	import Anchor from '$lib/Anchor.svelte';

	import { page } from '$app/stores';
	import { fly, blur } from 'svelte/transition';
	import { ArrowLeft, House, ReadCvLogo, Trophy } from 'phosphor-svelte';

	export let data;
</script>

{#if data.pathname !== '/'}
	<nav
		transition:fly={{ y: -56, delay: 240 }}
		class="fixed z-50 w-full border-b border-slate-600 border-opacity-10 bg-slate-50 bg-opacity-40 backdrop-blur-md"
	>
		<div class="mx-auto flex h-14 max-w-4xl items-center justify-between gap-4 px-4 sm:px-6">
			<NavItem link="/"><ArrowLeft /></NavItem>
			<!-- <div class="flex items-center gap-4 px-4 sm:px-6">
				<NavItem link="/achievement"><Trophy /></NavItem>
				<NavItem link="/cv"><ReadCvLogo /></NavItem>
			</div> -->
		</div>
	</nav>
{/if}
{#key data.pathname}
	<div in:blur={{ duration: 240, delay: 240, amount: 8 }} out:blur={{ duration: 120, amount: 16 }}>
		<div
			in:fly={{ x: 88, duration: 160, delay: 240 }}
			out:fly={{ x: -88, duration: 240 }}
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
