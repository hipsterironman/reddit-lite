<script>
    import { fade } from 'svelte/transition';
    export let thread;
</script>

<style>
    li {
        margin-bottom: 2vh;
        padding: .5vh 0;
        display: flex;
        justify-content: space-between;
        align-items: center;
        transition: opacity 1s;
    }
    
    div {
        display: flex;
        flex-direction: column;
    }

    a {
        display: inline-block;
    }

	.comments {
		font-size: .8em;
		font-style: italic;
	}
</style>

<li in:fade="{{ duration: 300 }}" out:fade="{{ duration: 100 }}">
    <div>
        <a href={thread.data.url}>{@html thread.data.title}</a>
        <a href={`https://reddit.com${thread.data.permalink}`} class="comments">Comments</a>
    </div>
</li>