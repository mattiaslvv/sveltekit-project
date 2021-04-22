<script>
	let name = '<i>Fat <b>Stonks</b></i>';
</script>

<svelte:head>
	<title>Portfolio</title>
</svelte:head>

<main>
	<div class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8" />
	<h1>{@html name}</h1>
	<h1>Portfolio</h1>
</main>

<style style lang="postcss">
	main {
		@apply text-center;
		@apply p-4;
		@apply mx-auto;
	}

	h1 {
		@apply text-red-600;
		@apply uppercase;
		@apply text-6xl;
		@apply font-thin;
		@apply leading-tight;
		@apply my-16 mx-auto;
		@apply max-w-xs;
	}

	p {
		@apply max-w-xs;
		@apply my-8 mx-auto;
		@apply leading-snug;
	}

	@screen sm {
		h1 {
			@apply max-w-none;
		}

		p {
			@apply max-w-none;
		}
	}
</style>
