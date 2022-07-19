<script>
    export let wordData = null;
    function playAudio(src) {
        let audio = new  Audio(src); 
        audio.play();
    }
</script>

<style>

</style>

<section class="word-data">
    {#if wordData.phonetics}
    <div class="audios">
        {#each wordData.phonetics as data}
        {#if data.audio !== ""}
            <div class="audio">
                <p>
                    {data.text}
                </p>
                <i class="fa fa-play-circle" on:click={() => playAudio(data.audio)}></i>
                
            </div>
        {/if}
        {/each}
    </div>
    {/if}
    
    {#if !wordData.phonetics}
    <div class="audio">
        No audio available
    </div>
    {/if}

    {#each wordData.meanings as meaning}
    <div class="meanings">
        <div class="pos">Part of Speech: {meaning.partOfSpeech}</div>
        <div class="definitions">
            {#each meaning.definitions as data, i}
            <div class="definition">
                <h2>{i + 1}. Definition: <b>{data.definition}</b></h2>
                {#if data.example}
                    <p>Example: <i>{data.example}</i></p>
                {/if}
            </div>
            {/each}
        </div>
    </div>
    {/each}

</section>