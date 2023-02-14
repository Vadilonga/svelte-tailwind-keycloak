<script lang="ts">
	import '../app.css';
	import { onMount } from 'svelte';
	import Keycloak from 'keycloak-js';

	let keycloak: Keycloak;
	let isAuth: boolean = false;
	let isLoading: boolean = true;

	onMount(async () => {
		keycloak = new Keycloak({
			realm: 'keycloak',
			url: 'http://localhost:8080',
			clientId: 'svelte-app'
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
	<div>loading</div>
{:else}
	<div>
		{#if isAuth}
			<main>
				<slot />
			</main>
		{:else}
			<div>Authentication failed</div>
		{/if}
	</div>
{/if}
