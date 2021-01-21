<script>
	import Modal from './Modal.svelte';
	import Post from './Post.svelte';
	import { onMount } from 'svelte';
	let threads = [];
	let subreddit = 'smashbros';
	let loadedSubreddit = subreddit;

	async function jsonTest() {
        threads = await fetch(`https://www.reddit.com/r/${subreddit}/top.json`)
            .then(r => r.json())
            .catch(err => console.log(err));
		threads = threads ? threads.data.children : [];
	}

	const handleSubmit = () => {
		loadedSubreddit = subreddit;
		jsonTest();
	}

    onMount(jsonTest);
</script>

<style>
	main {
		padding: 5vh 10vw;
	}

	ul {
		list-style: none;
		padding: 0;
		display: inline-block;
	}

	form {
		display: flex;
		margin-bottom: 5vh;
	}

	button {
		margin-left: 1vw;
	}

	h1 {
		margin-bottom: 1vh;
	}
</style>

<main>
	<h1>Reddit Lite</h1>
	<Modal />
	<h2>Here's what happened on /r/{loadedSubreddit} yesterday.</h2>

	<form on:submit|preventDefault={handleSubmit}>
		<input bind:value={subreddit}>
		<button type=submit>
			Load new subreddit
		</button>
	</form>

	<ul>
		{#each threads as thread (thread.data.id)}
			<Post thread={thread} />
		{/each}
	</ul>

	{#if threads.length === 0}
		<p>Looks like you entered a subreddit that doesn't exist.</p>
	{:else}
		<h2>You really didn't miss much. Now go do something else.</h2>
	{/if}
</main>
