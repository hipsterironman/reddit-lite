<script>
    import { fade } from 'svelte/transition';
    let isOpen = false;

    const open = () => isOpen = true;
    const close = () => isOpen = false;
</script>

<style>
    aside {
        color: rgb(0,100,200);
		font-size: .75em;
        font-style: italic;
        cursor: pointer;
        display: inline-block;
    }

    div.modal {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;

        display: flex;
        justify-content: center;
        align-items: center;
  }

  div.backdrop {
        position: absolute;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.4);
  }

  div.content-wrapper {
        z-index: 10;
        max-width: 50vw;
        border-radius: 0.3rem;
        background-color: white;
        overflow: hidden;
  }

  div.content {
        max-height: 50vh;
        overflow: auto;
        padding: 5vh 5vw;
  }

  @media (max-width: 500px) {
      div.content-wrapper {
          max-width: 70vw;
      }
  }
</style>

<aside on:click={open}>What is this?</aside>

{#if isOpen}
    <div transition:fade="{{ duration: 100 }}" class="modal" on:click={close}>
        <div class="backdrop" />
        <div class="content-wrapper">
            <div class="content">
                <p>I've been a member of Reddit since 2011.</p>
                <p>There hasn't been a day since where I haven't visited it.</p>
                <p>
                    This site is an attempt to break that streak. Enter a subreddit and the top posts of the past 24 
                    hours will load with links to both the content and the comments. This way, you can keep up with
                    what's happening with a lesser chance of being sucked in. You can fade out visited links to see
                    which you have left or unfade them to return later.
                </p>
                <p>Click anywhere to exit this box.</p>
            </div>
        </div>
    </div>
{/if}