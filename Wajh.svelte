<script>
  import AudioSection from "./AudioSection.svelte";

  export let wajhData;

</script>

<style>
  .wajh {
    max-width: 900px;
    margin: auto;
  }

  .wajh__image {
    width: 100%;
    height: auto;
  }

</style>

<div class="box wajh">
  <div class="columns">
    <div class="column is-8">
      <img src="http://www.quran-warch.org/warch/azrak/images/{wajhData.number}.gif"
        class="wajh__image"
        alt="wajh_{wajhData.number}">
    </div>

  <AudioSection wajhData="{wajhData}"  />
  </div>
</div>





