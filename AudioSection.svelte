<script>
  import FaRegPlayCircle from 'svelte-icons/fa/FaRegPlayCircle.svelte';
  import FaRegPauseCircle from 'svelte-icons/fa/FaRegPauseCircle.svelte'

  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  // export let audioNumber;
  export let wajhData;
  let start;
  let end;

  let audioPlayer;
  let audioTime;
  let startTime;
  let endTime;
  let id;

  $: audioPath = `http://www.quran-warch.org/warch/azrak/mp3/${wajhData.number}.mp3#t=${startTime},${endTime}`;
  $: isPlaying = (audioTime > startTime) && (audioTime < endTime) && (!audioPlayer.paused);

  function playHandler(aya) {
    startTime = parseSeconds(aya.start);
    endTime = parseSeconds(aya.end);
    id = aya.id;

    audioPlayer.load();
    audioPlayer.play();
  }

  function pauseHandler() {
    if (audioPlayer.paused) {
      audioPlayer.play();
    } else {
      audioPlayer.pause();
    }
  }

  function parseSeconds(timeTag) {
    let seconds = timeTag.split(":").reduce((acc, time) => 60 * acc + +time);
    return Number(seconds);
  }
</script>

<style>
  .pause {
    color: rgb(180, 180, 180);
  }

  .playing > .play{
    color: rgb(180, 180, 180);
  }
  .playing > .pause {
    color: black;
  }
  .icon {
    width: 2vw;
  }
</style>

<div class="column">
  <div class="columns is-multiline is-gapless">
    <div class="column is-full" id={wajhData.number}>
      <audio controls
        bind:this={audioPlayer}
        bind:currentTime={audioTime}
        preload="auto">
        <source src="{audioPath}"
          type="audio/mp3">
        <p>Your browser doesn't support HTML5 audio.</p>
      </audio>
    </div>

    {#each wajhData.ayat as aya, i (aya.id)}
      <div class="column is-full columns">
        <div class="column is-half"> {aya.id} </div>
        <div class="column is-half"
          class:playing="{ isPlaying  && aya.id === id }">
          <div on:click={ () => { playHandler(aya) } } class="icon play">
            <FaRegPlayCircle /> 
          </div>

          <div on:click={ pauseHandler } class="icon pause">
            <FaRegPauseCircle /> 
          </div>
        </div>
      </div>

    {/each}
  </div>
</div>

