<script lang="ts">
	import '../app.css';
	import { onMount } from 'svelte';
	import Keycloak from 'keycloak-js';

	let keycloak: Keycloak;
	let isAuth: boolean = false;
	let isLoading: boolean = true;
	/* create a .env file where you store VITE_KEYCLOAK_REALM, VITE_KEYCLOAK_URL and VITE_KEYCLOAK_CLIENT_ID*/
	onMount(async () => {
		keycloak = new Keycloak({
			realm: import.meta.env.VITE_KEYCLOAK_REALM,
			url: import.meta.env.VITE_KEYCLOAK_URL,
			clientId: import.meta.env.VITE_KEYCLOAK_CLIENT_ID
		});

		try {
			await keycloak.init({
				onLoad: 'login-required'
			});
			isAuth = true;
			console.log('User is authenticated');
		} catch (error) {
			isAuth = false;
			console.error(error);
		}
		isLoading = false;
	});
</script>

{#if isLoading}
<div class="text-center">
	<div class="fixed top-0 left-0 w-screen h-screen flex items-center justify-center">
        <svg aria-hidden="true" class="inline w-16 h-16 mr-2 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
            <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
        </svg>
        <span class="sr-only">Loading...</span>
    </div>
</div>
{:else}
	<div>
		{#if isAuth}
			<main>
				<slot />
			</main>
		{:else}
		<div class="fixed top-0 left-0 w-screen h-screen flex items-center justify-center">
			<div class="max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700">
				<a href="#">
					<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Authentication failed</h5>
				</a>
				<p class="mb-3 font-normal text-gray-700 dark:text-gray-400">Sorry, we couldn't log you in. Please check your email and password and try again.</p>
				<button type="button" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center inline-flex items-center mr-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
					<svg aria-hidden="true" class="w-5 h-5 mr-2 -ml-1" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">  
						<path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0zM4.501 20.118a7.5 7.5 0 0114.998 0A17.933 17.933 0 0112 21.75c-2.676 0-5.216-.584-7.499-1.632z"></path>
					</svg>
					Login
				  </button>
			</div>
		</div>
		{/if}
	</div>
{/if}
