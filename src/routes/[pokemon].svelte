<svelt:head>
	<title>{json.name}</title>
</svelt:head>


<div in:fade="{{delay:600}}" out:fade>

   <div>
      <button class="" onClick="history.go(-1); return false;">Back</button>
   </div>


	<div class="pokemon-container">

		<div class="pokemon-container-image">

			<img src="/art/{json.id}.png" alt="{json.name}">

		</div>

		<div class="pokemon-container-stats">

			<h1 class="title-case">{json.name}</h1>

         {#each json.types as object}
            <div class="title-case pokemon-type">{object.type.name}</div>
         {/each}

         <canvas id="myChart"></canvas>

		</div>

	</div>

   <div>

      <h1>Moves</h1>

      <select class="title-case" on:change="{getMove}">
         <option disabled selected>Select Move</option>
         {#each json.moves as move}
            <option value="{move.move.url}">{move.move.name.replace("-"," ")}</option>
         {/each}
      </select>

      {#if move}
         {move.power || 'N/A'}
         {move.pp}
         {move.name}
      {/if}

   </div>


</div>

<style>

   canvas {
   height: 100%;
   width: 500px;
   }

	img {
		width: 300px;
	}

	h1 {
		font-family: arial;
		font-size: 2rem;
		font-weight: 700;
		line-height: 1.5rem;
		text-align: left;
		padding-bottom: 1rem;
	}

	h2 {
		font-family: arial;
	}

	.pokemon-container {
		display: flex;
	}

	.pokemon-container-image {
		flex: 0 1 50%;
      margin: auto;
	}

	.pokemon-container-stats {
		flex: 0 1 50%;
		background: #FFFFFF;
		box-shadow: 0 10px 30px 0 rgba(74,144,226,0.15);
		border-radius: 8px;
		padding: 1rem;
	}

   .pokemon-type {
      padding: 0.4rem;
      background-color: #2EE59D;
      width: 6rem;
      height: 1.5rem;
      border-radius: 3rem;
      font-size: 0.8rem;
      text-align: center;
      display: flex;
      justify-content: center;
      align-items: center;
   }

	.title-case {
		text-transform: capitalize;
	}

   button {
      padding: 1rem;
      text-align: center;
      background-color: #2EE59D;
      color: #fff;
      border: none;
      border-radius: 4rem;
      margin: 1rem;
      padding: 1rem 2rem;
      box-shadow: 0px 8px 15px rgba(46, 229, 157, 0.4);
      font-family: arial;
      font-size: 0.8rem;
      transition: all 0.3s ease 0s;

   }

   button:hover {
      background-color: white;
      box-shadow: 0px 8px 15px rgba(74,144,226,0.15);
      color: black;
      /* transform: translateX(-7px); */
   }

   progress {
      border-radius: 2px;
      width: 100%;
      height: 0.5rem;
   }

   progress::-webkit-progress-bar {
      border-radius: 1rem
   }

   progress::-webkit-progress-value {
      border-radius: 1rem;
      background-color: #2EE59D;
   }

   progress::-moz-progress-bar {
   }

</style>

<script context="module">

	export async function preload(page) {

		const {params} = page;

		const json = await this.fetch('https://pokeapi.co/api/v2/pokemon/' + params.pokemon ).then(x => x.json());

		return {json}
	}
</script>

<script>

	import {fade} from 'svelte-transitions';
   import {onMount} from 'svelte';
   import Chart from 'chart.js';

   export let json;
   export let move;

   console.log(json);

   function toProperCase(str) {
       return str.replace(/\w\S*/g, function(txt){return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase();});
   };

   const labels = json.stats.map(item => toProperCase(item.stat.name.replace("-"," ")))

   const data = json.stats.map(item => item.base_stat)

   console.log(labels)

   onMount(async() => {

      var ctx = document.getElementById('myChart').getContext('2d');

      var myRadarChart = new Chart(ctx, {

         type: 'radar',
         data: {
            labels,
            datasets: [{
               data,
               pointBackgroundColor: '#2EE59D',
               backgroundColor: 'rgba(46,229,157,0.4)',
               borderColor: '#2EE59D',
            }],
         },
         
         options: {
            legend: {
               display: false
            },
         }
      });
   });

   async function getMove(e) {
      console.log(e.target.value)
      move = await fetch(e.target.value).then(x => x.json())
      console.log(move)
   }


</script>
