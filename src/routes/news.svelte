<script>
    import { onMount } from 'svelte';
    import Articles from './components/Articles.svelte';

    const newsAPI = import.meta.env.VITE_NEWS_KEY;

    onMount(async () => {
        getNews()
    });

    async function getNews() {
        return await fetch("https://api.github.com/users")
            .then(resp => resp.json())
    }

    let promise = getNews();

    function handleClick() {
        promise = getNews();
    }
</script>

<button on:click={ handleClick }>Go!</button>
{#await promise}
<p>Loading</p>
{:then stories}
  <Articles articles={stories}/>
{:catch error}
  <p>error</p>
{/await}

