<script>
    import translate from 'moji-translate';
    import { onMount } from 'svelte';
    import { isMaybeAlreadyAnEmoji } from 'moji-translate';

    let inp
    let translatedPhrase;
    let wrds;
    let wlist=[];
    let emlist = [];
    let copyv;
    let texttocopy;
    let copytoclip;

     onMount(() => {
        copytoclip =()=>{
            texttocopy = copyv.textContent;

            // Copy the text inside the text field
            navigator.clipboard.writeText(texttocopy);

            // Alert the copied text
            alert("Copied the text: " + copyText.value);
        }
    });

    function convert2moji(){
        // let ifinpmoji = isMaybeAlreadyAnEmoji(inp)
        // if(ifinpmoji){
            let emojis = translate.translate(inp,true);
            // Translate the phrase "the house is"
            translatedPhrase = emojis
            let wrds = inp.split(' ')
            wlist = []
            for (let i =0;i<wrds.length; i++){
                var word = wrds[i]+" "
                let emojisForWord = translate.getAllEmojiForWord(word);
                wlist.push({ word, emojis: emojisForWord });
                console.log(wlist)
            }

            console.log(emojis);
            console.log(translatedPhrase);
            
            // Get all emoji for the word '👀'
        // }
        // else{
        //     const emojis = translate.getAllEmojiForWord(inp);
        //     console.log(emojis)
        //     translatedPhrase = emojis
        // }
    }


</script>
<div class="main">
    <div class="nav">
        <div class="title">
            <h1>📖 Mojilang</h1>
            <p>Convert your text to emojis</p>
        </div>
    </div>
<input class="sbar" type="text" placeholder="Type a sentance..."  bind:value={inp} on:change={() => convert2moji()} name="" id="">
<!-- <h1>{translatedPhrase}</h1> -->
 {#if translatedPhrase}
    <button class="but" on:click={() => copytoclip()}>Copy to clipboard</button>
 {/if}
<div class="output" bind:this={copyv}>
    {#if translatedPhrase}
{#each wlist as item}
    {#if item.emojis !== ""}
        {#if item.emojis.length>1}
        <select class="sel">
            {#each item.emojis as tp}
                <option class="op" value={tp}>{tp}</option>
            {/each}
        </select>
        {:else}
            {#each item.emojis as tp}
            <h2 class="txt">{tp}</h2>
            {/each}
        {/if}
    {:else}
       <p class="txt">{item.word}</p>
    {/if}
{/each}
{:else}
    <p>Type something to translate</p>
{/if}
</div>
</div>

<div class="footer">
    <div class="madeby">
        <a href="https://anshwadhwa.vercel.app/">Made by Ansh Wadhwa</a>
    </div>
</div>
<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;600;700&display=swap');

* {
    font-family: 'Open Sans', sans-serif;
}
.txt{
    margin: 3px;
}
.nav{
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 40px;
    width: 100%;
    background-color: #398AB9;
    color: #ffffff;
}
.but{
  border: 0;
  background-color: #398AB9;
  padding: 10px;
  border-radius: 5px;
  color:#ffffff;
  margin-top: 10px;
  width: 60%;
}
.madeby{
    display: flex;
    justify-content: center;
}
.sbar{
    border: 0;
    border: 1;
    width: 70%;
    border-radius: 5px;
    padding: 15px;
    background-color: rgb(255, 255, 255);
}
.main{
    justify-content: center;
    text-align: center;
    padding: 0;
}
.sel{
    border-radius: 5px;
    font-size: 20px;
    border: 1;
    border-color: rgb(246, 246, 246);
    background-color: rgb(246, 246, 246);
    padding: 5px;
    margin: 2px;
}
.op{
    font-size: 20px;
}
.output{
    display: flex;
    border: 0;
    flex-wrap: wrap;
    margin-bottom: 30px;
    justify-content: center;
    border-radius: 5px;
    margin-left: 16%;
    align-items: center;
    margin-top: 30px;
    width: 70%;
    text-align: center;
    overflow-wrap: break-word;
    unicode-bidi: isolate;
    background-color: rgb(255, 255, 255);
    padding: 10px;
}
</style>