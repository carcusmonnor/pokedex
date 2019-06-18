<a class="grid-card" href="{data.name}">
   <h1 class="title">
      <span>{id}:</span>
      {data.name}
   </h1>

   <!-- {#if} statement is for the imageCheck function below -->

   <!-- {#if imageCheck(`/art/${getId(result.url)}.png`)} -->
      <a href="{data.name}" sapper-noscroll>
         <img src="/art/{id}.png">
      </a>
   <!-- {/if} -->
</a>

<script>

   export let data;
   export let id;

</script>

<style>

   span {
      font-weight: bold;
   }

   .title {
      font-size: 1.5rem;
      text-transform: capitalize;
      white-space: nowrap;
   }

   .grid-card {
      background: #FFFFFF;
      box-shadow: 0 10px 30px 0 rgba(74,144,226,0.15);
      border-radius: 8px;
      margin: 0.5rem;
      padding: 1rem;
      transition: all 0.3s ease 0s;
   }

   .grid-card:hover {
      box-shadow: 0px 8px 15px rgba(74,144,226,0.15);
      transform: translateY(-7px);
   }

</style>