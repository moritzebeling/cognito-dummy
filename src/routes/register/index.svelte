<script context="module">
	export async function load({ session }) {
		if (session.user) {
			return { redirect: '/', status: 302 };
		}
		return {};
	}
</script>

<script>
	import { session } from '$app/stores';
	import { goto } from '$app/navigation';
	import { post } from '$lib/utils.js';
	import ListErrors from '$lib/ListErrors.svelte';

	let username = '';
	let email = '';
	let password = '';
	let errors = null;

	async function submit(event) {
		const response = await post(`auth/register`, { username, email, password });

		// TODO handle network errors
		errors = response.errors;

		if (response.user) {
			$session.user = response.user;
			goto('/');
		}
	}
</script>

<svelte:head>
	<title>Sign up • Conduit</title>
</svelte:head>

<h1>Sign up</h1>
<p>
	<a href="/login">Have an account?</a>
</p>

<ListErrors {errors}/>

<form on:submit|preventDefault={submit}>

	<label>
		<p>Your Name</p>
		<input type="text" required placeholder="Your Name" bind:value={username}>
	</label>

	<label>
		<p>Email</p>
		<input type="email" required placeholder="Email" bind:value={email}>
	</label>

	<label>
		<p>Choose a secure password</p>
		<input type="password" required minlength="8" placeholder="Password" bind:value={password}>
	</label>

	<button>Sign up</button>

</form>
