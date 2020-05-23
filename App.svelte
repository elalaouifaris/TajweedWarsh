<script>
  import "bulma/css/bulma.css";
  import Wajh from "./Wajh.svelte";

  export let dataset;

  let selectedWajh = "001";

  let wajhList = Object.keys(dataset);
  $: wajhData = dataset[selectedWajh];
</script>

<style>
  main {
    font-family: sans-serif;
    text-align: center;
  }
</style>

<main>
	<h1>Tajweed Warsh</h1>
 <select bind:value={selectedWajh} name="wajh" id="wajh-seletion">
    {#each wajhList as wajh_nb}
      <option value="{wajh_nb}">{wajh_nb}</option>
    {/each}
  </select>
  
  <h2>Wajh {selectedWajh}</h2>
  <Wajh wajhData={wajhData} />
</main>
