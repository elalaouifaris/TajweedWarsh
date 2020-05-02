<script>
  import { afterUpdate } from "svelte";
  import AudioSection from "./AudioSection.svelte";

  export let wajhData;
  let audioPlayer;

  afterUpdate(() => {
    audioPlayer.load();
  });
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

    <div class="column">
      <div class="columns is-multiline">
        <div class="column is-full" id={wajhData.number}>
          <audio controls
            bind:this={audioPlayer}
            preload="auto">
            <source src="http://www.quran-warch.org/warch/azrak/mp3/{wajhData.number}.mp3"
              type="audio/mp3">
            <p>Your browser doesn't support HTML5 audio.</p>
          </audio>
        </div>

        {#each wajhData.ayat as aya, i (aya.id)}
          <div class="column is-half">
            <h3>Aya {i}: {aya.id}</h3>
            <AudioSection
              audioNumber={wajhData.number}
              start={aya.start}
              end={aya.end} />
          </div>
    
        {/each}
      </div>
    </div>
  </div>
</div>





