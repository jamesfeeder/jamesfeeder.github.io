<script>
	import Anchor from '$lib/Anchor.svelte';
	import { onMount } from 'svelte';

	let scrollY = 0;
	let innerHeight = 0;
	let innerWidth = 0;

	let scrollbarWidth = 0;

	onMount(() => {
		scrollbarWidth = window.innerWidth - document.documentElement.clientWidth;
	});
</script>

<svelte:head>
	<title>jamesfeeder's home</title>
</svelte:head>

<!-- <code class="fixed left-0 top-0 z-[100]">Scroll Y: {scrollY} px <br /></code> -->

<svelte:window bind:scrollY bind:innerHeight bind:innerWidth />

<!-- max-w-4xl -->
<main
	class="sticky top-0 mx-auto flex min-h-screen max-w-fit flex-col justify-center"
	style={`
		filter: blur(${Math.min(scrollY / 50, 8)}px);
		opacity: ${1 - Math.min(scrollY / (0.2 * innerHeight), 1)};
		transform: perspective(1200px) translatez(${-scrollY / 2}px);
	`}
>
	<div class="p-6 pb-24">
		<h1 class="text-3xl font-semibold text-slate-800 sm:text-[2rem] md:text-[2.5rem]">
			Jetsadakorn Maliwan
		</h1>
		<div class="flex flex-wrap items-center gap-1.5 py-4">
			<p class="font-light text-slate-500">Software Developer /</p>
			<p class="font-light text-slate-500">Front-End Web Developer</p>
		</div>
		<div class="flex flex-wrap items-center gap-6 gap-y-1 sm:gap-8">
			<Anchor label="GitHub Profile" link="https://github.com/jamesfeeder" openNewTab />
			<Anchor label="Curriculum Vitae" link="/cv" />
		</div>
	</div>
</main>
