<script>
    import { onMount } from 'svelte';
    onMount(async () => {
        getNews()
    });

    async function getNews() {
        const res = fetch('https://quickchart.io/wordcloud', {
            method: 'POST',
            headers: {
                format: 'png',
                width: 1000,
                height: 1000,
                fontScale: 15,
                scale: 'linear',
                removeStopwords: true,
                minWordLength: 4,
                text: article
            }
        });

    }
</script>
