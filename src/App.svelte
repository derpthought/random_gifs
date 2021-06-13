<script lang="ts">
	let name: string = 'cat';
	const url_base:string = "https://api.giphy.com/v1/gifs/random?api_key=iJVP0zYSmEKGwV29vvtpe6ghe207Jfsq&tag=";
	var url = url_base + name;
	
	async function getGIF(URL:string) {
		const res = await fetch(url);
		const gifJSON = await res.json();
		const gifURL = gifJSON.data.image_url;
		console.log("Outputting JSON...", gifJSON);
		console.log("Outputting URL...", gifURL);

		if(res.ok){
			return gifURL;
		} else {
			throw new Error("Something is broken!");
		}	
	}

	let promise = getGIF(url);

	function handleInput(){
		url = url_base + name;
		promise = getGIF(url);
	}
		
</script>

<input bind:value={name}>
<button on:click={handleInput}>Search</button>
{#await promise}
	<p>"Loading GIF..."</p>
{:then gif}
	<img src={gif} alt="{name} gif" width="100%">
{/await}

