<script lang="ts">
	import Anchor from '$lib/Anchor.svelte';
</script>

<svelte:head>
	<title>jamesfeeder's home</title>
</svelte:head>

<!-- max-w-4xl -->
<main class="sticky top-0 mx-auto flex min-h-screen max-w-fit flex-col justify-center">
	<div class="p-6 pb-24">
		<h1 class="text-center text-3xl font-semibold text-slate-800 sm:text-[2rem] md:text-[2.5rem]">
			Jetsadakorn Maliwan
		</h1>
		<div class="flex flex-wrap items-center justify-center gap-1.5 py-4">
			<p class="font-light text-slate-500">Software Developer /</p>
			<p class="font-light text-slate-500">Front-End Web Developer</p>
		</div>
		<div class="flex flex-wrap items-center justify-center gap-6 gap-y-1 sm:gap-8">
			<Anchor label="GitHub Profile" link="https://github.com/jamesfeeder" openNewTab />
			<Anchor label="Curriculum Vitae" link="/cv" />
		</div>
	</div>
</main>
