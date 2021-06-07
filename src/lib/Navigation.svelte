<script>

	import { session } from '$app/stores';
	import { post } from '$lib/utils.js';

	async function logout() {
		await post(`auth/logout`);

		// this will trigger a redirect, because it
		// causes the `load` function to run again
		$session.user = null;
	}

</script>

<nav>

    <a sveltekit:prefetch href="/">Home</a>
    <a sveltekit:prefetch href="/public">Public</a>

	{#if $session.user}

		<button on:click={logout}>Logout</button>

	{:else}

		<a sveltekit:prefetch href="/register">Register</a>
		<a sveltekit:prefetch href="/login">Login</a>

	{/if}

</nav>
