<!-- <header>

   <form on:submit={search}>

      <input bind:value="{query}">Search</input>

   </form>

</header> -->

<main>

   <slot></slot>

</main>

<script>

	export let segment;

   // let query;
   //
   // function search() {
   //
   //       const json =  fetch(`https://pokeapi.co/api/v2/pokemon?limit=1000`).then(x => x.json());
   //
   //       if ('key' in myObj)
   // }

</script>

