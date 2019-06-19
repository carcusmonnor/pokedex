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

			<h2>Statistics</h2>

			<div>

				{#each json.stats as item}
					<p class="title-case">{item.stat.name}:</p>
               <progress min="0" max="255" value="{item.base_stat}"></progress>
				{/each}

			</div>

		</div>

	</div>

   <div>

      <h1>Moves</h1>

      {#each json.moves as move}
         <p class="title-case">{move.move.name}</p>
      {/each}

   </div>

</div>

<style>
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
	export let json
</script>
