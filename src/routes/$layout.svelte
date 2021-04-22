<script>
	import '../app.postcss';
	import Navbar from '$lib/Navbar.svelte';
	import Footer from '$lib/Footer.svelte';
</script>

<div class="flex flex-col h-screen">
	<Navbar
		links={[
			{ name: 'Home', link: '/' },
			{ name: 'My watched stocks', link: '/stocks' },
			{ name: 'Reports', link: '/reports' },
			{ name: 'My portfolio', link: '/portfolio' }
		]}
	/>
	<main class="flex-grow">
		<slot />
	</main>
	<Footer />
</div>
