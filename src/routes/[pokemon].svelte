<svelt:head>
	<title>{json.name}</title>
</svelt:head>


<div in:fade="{{delay:4000}}" out:fade>

   <div>
      <button onClick="history.go(-1); return false;">Back</button>
   </div>


	<div class="pokemon-container">

		<div class="pokemon-container--child">
			<img src="/art/{json.id}.png">
		</div>

		<div class="pokemon-container--child">

			<h1 class="title-case">{json.name}</h1>

			<h2>Statistics</h2>

			<div>

				{#each json.stats as item}
					<p class="title-case"><span>{item.stat.name}:</span> {item.base_stat}</p>
				{/each}

			</div>

		</div>

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

	span {
		font-family: arial;
		font-weight: 700;
		letter-spacing: 1px;
		text-transform: uppercase;
	}

	.pokemon-container {
		display: flex;
	}

	.pokemon-container--child {
		flex: 0 1 50%;
	}

	.pokemon-container--child:last-child {
		background: #FFFFFF;
		box-shadow: 0 10px 30px 0 rgba(74,144,226,0.15);
		border-radius: 8px;
		padding: 1rem;
	}

	.title-case {
		text-transform: capitalize;
	}

   .button {
      padding: 1rem;
      text-align: center;
   }

   button {
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
	console.log(json)
</script>
