<script>
	import Wordbase from './wordbase.svelte';
	import Loader from './loader.svelte';

	let word = "";
	let loading = false;
	let wordData = null;

	async function searchWord(){
		if (word.length === 0) {
			return;
		}
		loading = true;
		wordData = null;
		try{
			let res = await fetch("https://api.dictionaryapi.dev/api/v2/entries/en/"+word);
			let data = await res.json();
			if(Array.isArray(data)){
				wordData = data[0];
			} else {
				wordData = "E no dey dictionary na";
			}
			loading = false;
		}
		catch(err){
			loading = false;
		}
	}

	function enterclick(){
  		if (event.key === "Enter") {
    		event.preventDefault();
    		// Trigger the button element with a click
    		document.getElementById("btn").click();
  		}
	};
	
</script>

<main>
	<header>
		<h1><i class="fa fa-book"></i><br>Word Hokage</h1>
		<h4>A Dictionary built using Svelte</h4>
		<section class="input-word">
			<input type="text" id="word" placeholder="Enter a word to search" bind:value={word} on:keydown={enterclick}/>
			<button id="btn" on:click={searchWord}>Search</button>
		</section>
	</header>
	
	<section class="content">
		{#if loading === true || wordData !== null}
		<div class="result">
			{#if  wordData !== null && typeof wordData !== "string"}
			<Wordbase wordData={wordData} />
			{:else if wordData === null && loading === true}
			<Loader />
			{:else}
			<p>Omo we no see the meaning o</p>
			{/if}
		</div>
		{/if}
	</section>	

	<footer>
		Built by <span>Jolliano</span>
	</footer>
</main>