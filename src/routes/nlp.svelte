<script>
    let disabled = false;
    let res = '';
    let promise = Promise.resolve([]);

    var raw = "I am a string"

    const requestOptions = {
        method: 'POST',
        headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
        },
        body: raw
    };
     
	async function getSentiment() {
	    const res = await fetch('https://ethicailly.herokuapp.com/sentiment', requestOptions);
        if (res.ok) {
  		    return res.json();	
		} else {
			throw new Error();
		}
	} 
/*
    function getSentiment() {
        const fetchImage = (async () => {
		    const response = await fetch('https://ethicailly.herokuapp.com/sentiment', requestOptions)
            return await response.json()
        })()
    }*/

	function handleClick() {
	    //promise = getSentiment();
        const response = (async () => {
		    const response = await fetch('https://ethicailly.herokuapp.com/sentiment', requestOptions)
            return await response.json()
        })()
        disabled = true;
	}
</script>

<button on:click={handleClick} {disabled}>Click</button>

{#await handleClick}
	<p>...waiting</p>
{:then data}
	<p>
        {data.toString}
    </p>
{:catch error}
	<p>An error occurred!</p>
{/await}
