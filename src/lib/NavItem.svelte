<script lang="ts">
	import { page } from '$app/stores';
	import { targetUrlStore } from './stores';

	
	interface Props {
		link: string;
		children?: import('svelte').Snippet;
	}

	let { link, children }: Props = $props();
</script>

<a
	href={link}
	onclick={() => {
		targetUrlStore.update((url) => (url = link));
	}}
	class="relative flex h-12 w-12 items-center justify-center rounded-md text-3xl text-slate-800 transition-all hover:bg-slate-600 hover:bg-opacity-10 aria-[current=true]:text-blue-600 dark:text-slate-200"
	aria-current={$page.url.pathname === link}>{@render children?.()}</a
>
