<a class="grid-card" href="{data.name}">

   <h1 class="title">
      {data.name}
   </h1>

   <!-- {#if} statement is for the imageCheck function below -->

   <!-- {#if imageCheck(`/art/${getId(result.url)}.png`)} -->
      <a href="{data.name}" sapper-noscroll>
         <img src="/art/{id}.png" alt="{data.name}">
      </a>
   <!-- {/if} -->

   <div>
      <div class="id-dot">{id}</div>
   </div>

</a>

<script>

   export let data;
   export let id;

</script>

<style>

   .id-dot {
      display: flex;
      width: 2rem;
      height: 2rem;
      border-radius: 1rem;
      background: #242430;
      color: #2EE59D;
      font-weight: bold;
      line-height: 1;
      justify-content: center;
      align-items: center;
      margin: 0 auto -4rem auto;
   }

   .title {
      font-size: 1.5rem;
      text-align: center;
      text-transform: capitalize;
      white-space: nowrap;
   }

   .grid-card {
      background: #FFFFFF;
      box-shadow: 0 10px 30px 0 rgba(74,144,226,0.15);
      border-radius: 8px;
      margin: 0.9rem 0.6rem;
      padding: 1rem 1rem 3rem 1rem;
      transition: all 0.3s ease 0s;
   }

   .grid-card:hover {
      box-shadow: 0px 8px 15px rgba(74,144,226,0.15);
      transform: translateY(-7px);
   }

</style>