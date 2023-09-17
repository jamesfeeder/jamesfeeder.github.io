<!-- <head>
	<title>jamesfeeder</title>
</head> -->

<script>
	import Anchor from '$lib/Anchor.svelte';
</script>

<main class="flex min-h-screen flex-col justify-center">
	<div class="w-3xl mx-auto p-6 transition-all">
		<h1 class="text-3xl font-semibold text-slate-800 sm:text-[2rem] md:text-[2.5rem]">
			Jetsadakorn Maliwan
		</h1>
		<div class="flex flex-wrap items-center gap-1.5 py-4">
			<p class="font-semibold text-slate-500">Software Developer /</p>
			<p class="font-semibold text-slate-500">Front-End Web Developer</p>
		</div>
		<div class="flex flex-wrap items-center gap-6 gap-y-1 sm:gap-8">
			<Anchor label="GitHub Profile" link="https://github.com/jamesfeeder" openNewTab />
			<Anchor label="Résumé" link="/resume" />
		</div>
	</div>
</main>
