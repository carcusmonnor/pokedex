<div in:fade="{{delay:500}}" out:fade>

   <div class="grid-layout">

   	{#each json.results as result}
         <Card data="{result}" id="{getId(result.url)}"/>
   	{/each}

      {#if more}

         {#each more as result}
            <Card data="{result}" id="{getId(result.url)}"/>
         {/each}

      {/if}

   </div>

   <div class="button">

      <button on:click="{loadMore}">Load More</button>

   </div>

</div>


<style>

   .button {
      padding: 1rem;
      text-align: center;
   }

   button {
      background-color: white;
      border: none;
      border-radius: 4rem;
      margin: 1rem;
      padding: 1rem 2rem;
      box-shadow: 0px 8px 15px rgba(74,144,226,0.15);
      font-family: arial;
      font-size: 0.8rem;
      transition: all 0.3s ease 0s;

   }

   button:hover {
      background-color: #2EE59D;
      box-shadow: 0px 8px 15px rgba(46, 229, 157, 0.4);
      color: #fff;
      transform: translateY(-7px);
   }

   .grid-layout {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      max-width: 1200px;
   }

</style>

<!-- If the limit is set >720(number of pokemon with images) it will throw out 404 errors -->

<script context="module">
   let count = 10;

	export async function preload() {

		const json = await this.fetch('https://pokeapi.co/api/v2/pokemon?limit=' + count).then(x => x.json());

		return {json, count}
	}
</script>

<script>

	import {fade} from 'svelte-transitions';
   import Card from '../components/Card.svelte'

	export let json
	console.log(json)
   let more = []

   export let count;
   let offset = count;

   // The function below is to stop it loading an image when there isnt one.

   // function imageCheck(img){
   //    if (process.browser){
   //       var image = new Image();
   //       image.src = img;
   //       return (image.height != 0);
   //    }
   //    else {return false}
   // }

   async function loadMore(){
      const json = await fetch(`https://pokeapi.co/api/v2/pokemon?limit=${count}&offset=${offset}`).then(x => x.json());

      more = [...more, ...json.results]
      offset = offset + count;
      console.log(json)

   }

   function getId(url){
      let parts = url.split('/')
      return parts.pop() || parts.pop()
   }
</script>
