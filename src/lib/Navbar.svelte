<script>
	import Navlink from '$lib/Navlink.svelte';
	import { clickOutside } from '$lib/clickOutside.js';
	import Transition from 'svelte-class-transition';
	import { userLoggedInStore } from '$lib/stores/stores';
	export let links = [{}];
	export let showMenu = false;
	let timeout = false;
	let isUserLoggedIn;
	$: {
		userLoggedInStore.subscribe((value) => {
			isUserLoggedIn = value;
		});
	}
	function toggleMenu() {
		if (showMenu !== true && !timeout) {
			showMenu = !showMenu;
		}
	}
	function handleOutsideClick(e) {
		if (showMenu === true) {
			showMenu = false;
		}
		timeout = true;
		setTimeout(() => {
			timeout = false;
		}, 200);
	}
</script>

<div class="sticky">
	<nav class="bg-gradient-to-r from-gray-800 to-green-600">
		<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
			<div class="flex items-center justify-between h-16">
				<div class="flex items-center">
					<div class="flex-shrink-0">
						<svg
							xmlns="http://www.w3.org/2000/svg"
							class="h-10 w-10"
							fill="none"
							viewBox="0 0 24 24"
							stroke="white"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M16 8v8m-4-5v5m-4-2v2m-2 4h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"
							/>
						</svg>
					</div>
					<p class="text-white px-3 py-2 rounded-md text-sm font-small">
						<i>Fat <b>Stonks</b></i>
					</p>
					<div class="hidden md:block">
						<div class="ml-10 flex items-baseline space-x-4">
							{#each links as link}
								<Navlink {...link} mobile={false} />
							{/each}
						</div>
					</div>
				</div>
				<!-- If user is logged in, show his profile & a dropwdown menu -->
				{#if isUserLoggedIn}
					<div class="hidden md:block">
						<div class="ml-4 flex items-center md:ml-6">
							<button
								class="bg-gray-800 p-1 rounded-full text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white"
							>
								<span class="sr-only">View notifications</span>
								<!-- Heroicon name: outline/bell -->
								<svg
									class="h-6 w-6"
									xmlns="http://www.w3.org/2000/svg"
									fill="none"
									viewBox="0 0 24 24"
									stroke="currentColor"
									aria-hidden="true"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
									/>
								</svg>
							</button>

							<!-- Profile dropdown -->
							<div class="ml-3 relative">
								<div>
									<button
										type="button"
										class="max-w-xs bg-gray-800 rounded-full flex items-center text-sm focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white"
										aria-expanded="false"
										aria-haspopup="true"
										id="user-menu-button"
										on:click={toggleMenu}
									>
										<span class="sr-only">Open user menu</span>
										<img
											class="h-8 w-8 rounded-full"
											src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
											alt=""
										/>
									</button>
								</div>

								<!-- Dropdown menu -->
								{#if showMenu}
									<Transition
										{showMenu}
										transitions="transition transform"
										inTransition="ease-out duration-80"
										inState="opacity-0 scale-95"
										onState="opacity-100 scale-100"
										outState="opacity-0 scale-95"
										outTransition="ease-in duration-60"
									>
										<div
											class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg py-1 bg-white ring-1 ring-black ring-opacity-5 focus:outline-none"
											role="menu"
											id="user-menu"
											aria-orientation="vertical"
											aria-labelledby="user-menu-button"
											tabindex="-1"
											use:clickOutside
											on:click_outside={handleOutsideClick}
										>
											<!-- TODO:FIXME:TODO: -->
											<a
												href="/profile"
												class="block px-4 py-2 text-sm text-gray-700"
												role="menuitem"
												tabindex="-1"
												id="user-menu-item-0"
												on:click={showMenu}>Your Profile</a
											>

											<a
												href="/settings"
												class="block px-4 py-2 text-sm text-gray-700"
												role="menuitem"
												tabindex="-1"
												id="user-menu-item-1"
												on:click={showMenu}>Settings</a
											>

											<a
												href="#"
												class="block px-4 py-2 text-sm text-gray-700"
												role="menuitem"
												tabindex="-1"
												id="user-menu-item-2"
												on:click={showMenu}>Sign out</a
											>
										</div>
									</Transition>
								{/if}
							</div>
						</div>
					</div>
				{/if}
				<!-- if user is not logged in, show login link -->
				{#if !isUserLoggedIn}
					<a
						href="/login"
						class="flex items-center text-gray-300 hover:bg-gray-700 block hover:text-white px-3 py-2 rounded-md text-sm font-medium"
						sveltekit:prefetch
						>Log in <div class="flex-shrink-0">
							<svg
								xmlns="http://www.w3.org/2000/svg"
								class="h-6 w-6 ml-2"
								fill="none"
								viewBox="0 0 24 24"
								stroke="currentColor"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1"
								/>
							</svg>
						</div></a
					>
				{/if}
				<div class="-mr-2 flex md:hidden">
					<!-- Mobile menu button -->
					<button
						type="button"
						class="bg-gray-800 inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white"
						aria-controls="mobile-menu"
						aria-expanded="false"
					>
						<span class="sr-only">Open main menu</span>
						<!-- TODO:FIXME:TODO: -->
						<!--
                Heroicon name: outline/menu
  
                Menu open: "hidden", Menu closed: "block"
              -->
						<svg
							class="block h-6 w-6"
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke="currentColor"
							aria-hidden="true"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M4 6h16M4 12h16M4 18h16"
							/>
						</svg>
						<!-- TODO:FIXME:TODO: -->
						<!--
                Heroicon name: outline/x
  
                Menu open: "block", Menu closed: "hidden"
              -->
						<svg
							class="hidden h-6 w-6"
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke="currentColor"
							aria-hidden="true"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M6 18L18 6M6 6l12 12"
							/>
						</svg>
					</button>
				</div>
			</div>
		</div>

		<!-- TODO:FIXME:TODO: -->
		<!-- Mobile menu, show/hide based on menu state. -->
		<div class="md:hidden" id="mobile-menu">
			<div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
				{#each links as link}
					<Navlink {...link} mobile={true} />
				{/each}
			</div>
			<div class="pt-4 pb-3 border-t border-gray-700">
				<div class="flex items-center px-5">
					<div class="flex-shrink-0">
						<img
							class="h-10 w-10 rounded-full"
							src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
							alt=""
						/>
					</div>
					<div class="ml-3">
						<div class="text-base font-medium leading-none text-white">Tom Cook</div>
						<div class="text-sm font-medium leading-none text-gray-400">tom@example.com</div>
					</div>
					<button
						class="ml-auto bg-gray-800 flex-shrink-0 p-1 rounded-full text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white"
					>
						<span class="sr-only">View notifications</span>
						<!-- Heroicon name: outline/bell -->
						<svg
							class="h-6 w-6"
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke="currentColor"
							aria-hidden="true"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
							/>
						</svg>
					</button>
				</div>
				<div class="mt-3 px-2 space-y-1">
					<!-- TODO:FIXME:TODO: -->
					<a
						href="#"
						class="block px-3 py-2 rounded-md text-base font-medium text-gray-400 hover:text-white hover:bg-gray-700"
						>Your Profile</a
					>

					<a
						href="#"
						class="block px-3 py-2 rounded-md text-base font-medium text-gray-400 hover:text-white hover:bg-gray-700"
						>Settings</a
					>

					<a
						href="#"
						class="block px-3 py-2 rounded-md text-base font-medium text-gray-400 hover:text-white hover:bg-gray-700"
						>Sign out</a
					>
				</div>
			</div>
		</div>
	</nav>
</div>
