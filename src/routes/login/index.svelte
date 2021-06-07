<script context="module">
	export async function load({ session }) {
		if (session.user) {
			return {
				status: 302,
				redirect: '/'
			};
		}

		return {};
	}
</script>

<script>
	import { session } from '$app/stores';
	import { goto } from '$app/navigation';
	import { post } from '$lib/utils.js';
	import ListErrors from '$lib/ListErrors.svelte';

	let email = '';
	let password = '';
	let errors = null;

	async function submit(event) {
		const response = await post(`auth/login`, { email, password });

		// TODO handle network errors
		errors = response.errors;

		if (response.user) {
			$session.user = response.user;
			goto('/');
		}
	}
</script>

<svelte:head>
	<title>Sign in • Conduit</title>
</svelte:head>

<h1>Sign In</h1>
<p>
	<a href="/register">Need an account?</a>
</p>

<ListErrors {errors}/>

<form on:submit|preventDefault={submit}>

	<label>
		<p>Email</p>
		<input type="email" required placeholder="Email" bind:value={email}>
	</label>

	<label>
		<p>Password</p>
		<input type="password" required placeholder="Password" bind:value={password}>
	</label>

	<button type="submit">
		Sign in
	</button>

</form>
