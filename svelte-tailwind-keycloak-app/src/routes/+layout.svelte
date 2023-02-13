<script lang='ts'>
  import "../app.css";
  import { onMount } from 'svelte';
  import Keycloak from 'keycloak-js';

    let keycloak: Keycloak;
    export let isAuth = false;
    
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
        isAuth=true;
        console.log('User is authenticated');
      } catch (error) {
        console.error(error);
      }
    });

</script>
{#if isAuth}
<main>
  <slot/>
</main>
{:else}
Authentication failed
{/if}


