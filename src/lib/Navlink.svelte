<script>
	export let name;
	export let link;
	export let mobile;
	import { page } from '$app/stores';
	let anchorClass;
	$: {
		if ($page.path === link && !mobile) {
			anchorClass = 'bg-gray-900 text-white px-3 py-2 rounded-md text-sm font-small';
		} else if (!mobile) {
			anchorClass =
				'text-gray-300 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-medium';
		}
		if ($page.path === link && mobile) {
			anchorClass = 'bg-gray-900 text-white block px-3 py-2 rounded-md text-base font-medium';
		} else if (mobile) {
			anchorClass =
				'text-gray-300 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-medium';
		}
	}
</script>

{#if !mobile}
	<a class:anchorClass={$page.path === link} href={link} class={anchorClass} sveltekit:prefetch
		>{name}</a
	>
{/if}

{#if mobile}
	<a class={anchorClass} class:anchorClass={$page.path === link} href={link} sveltekit:prefetch
		>{name}
	</a>
{/if}
