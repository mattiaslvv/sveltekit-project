<script>
	let name = '<i>Fat <b>Stonks</b></i>';
</script>

<svelte:head>
	<title>Login</title>
</svelte:head>
<!-- <div class="min-h-screen flex items-center justify-center bg-gray-50 py-12 px-4 sm:px-6 lg:px-8"></div> -->

<main>
	<div class="flex justify-center max-w-7xl mx-auto mt-20 py-6 sm:px-6 lg:px-8">
		<div class="max-w-md w-full space-y-8">
			<div>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					class="mx-auto h-12 w-auto"
					fill="none"
					viewBox="0 0 24 24"
					stroke="currentColor"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M16 8v8m-4-5v5m-4-2v2m-2 4h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"
					/>
				</svg>
				<h1 class="text-center text-1xl text-red-600">{@html name}</h1>
				<h2 class="mt-6 text-center text-3xl font-extrabold text-gray-900">
					Sign in to your account
				</h2>
				<p class="mt-2 text-center text-sm text-gray-600">
					Or start
					<a href="#" class="font-medium text-base transition text-gray-600 hover:text-green-600">
						your 14-day free trial
					</a>
				</p>
			</div>
			<form class="mt-8 space-y-6" action="#" method="POST">
				<input type="hidden" name="remember" value="true" />
				<div class="rounded-md shadow-sm -space-y-px">
					<div>
						<label for="email-address" class="sr-only">Email address</label>
						<input
							id="email-address"
							name="email"
							type="email"
							autocomplete="email"
							required
							class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-red-600 focus:border-green-600 focus:z-10 sm:text-sm"
							placeholder="Email address"
						/>
					</div>
					<div>
						<label for="password" class="sr-only">Password</label>
						<input
							id="password"
							name="password"
							type="password"
							autocomplete="current-password"
							required
							class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-b-md focus:outline-none focus:ring-red-600 focus:border-green-600 focus:z-10 sm:text-sm"
							placeholder="Password"
						/>
					</div>
				</div>

				<div class="flex items-center justify-between">
					<div class="flex items-center">
						<input
							id="remember_me"
							name="remember_me"
							type="checkbox"
							class="h-4 w-4 text-red-600 focus:ring-red-600 border-gray-300 rounded"
						/>
						<label for="remember_me" class="ml-2 block text-sm text-gray-900"> Remember me </label>
					</div>

					<div class="text-sm">
						<a href="#" class="font-medium text-gray-600 hover:text-red-600 hover:ring-green-600">
							Forgot your password?
						</a>
					</div>
				</div>

				<div>
					<button
						type="submit"
						class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white transition bg-gray-600 duration-200 ease-in-out hover:bg-green-600 transform-gpu hover:scale-110 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
					>
						<span class="absolute left-0 inset-y-0 flex items-center pl-3">
							<!-- Heroicon name: solid/lock-closed -->
							<svg
								class="h-5 w-5 text-white group-hover:text-white"
								xmlns="http://www.w3.org/2000/svg"
								viewBox="0 0 20 20"
								fill="currentColor"
								aria-hidden="true"
							>
								<path
									fill-rule="evenodd"
									d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z"
									clip-rule="evenodd"
								/>
							</svg>
						</span>
						Sign in
					</button>
				</div>
			</form>
		</div>
	</div>
</main>
