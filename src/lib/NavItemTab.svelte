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
	class="relative flex h-12 w-12 items-center justify-center overflow-clip  rounded-md text-3xl transition-all after:absolute after:bottom-0 after:h-1 after:w-0 after:rounded-full after:bg-transparent after:transition-all hover:bg-slate-600 hover:bg-opacity-10 hover:after:w-1 hover:after:bg-blue-400 aria-[current=true]:after:w-4 aria-[current=true]:after:bg-blue-600"
	aria-current={$page.url.pathname === link}>{@render children?.()}</a
>
