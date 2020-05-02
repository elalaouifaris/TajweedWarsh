<script>
  export let audioNumber;
  export let start;
  export let end;

  let audio;
  let startTime = parseSeconds(start);
  let endTime = parseSeconds(end);
  let audioTime = startTime;

  let audioPath = `http://www.quran-warch.org/warch/azrak/mp3/${audioNumber}.mp3#t=${start},${end}`;

  function playHandler() {
    audio.load();
    audio.play();
  }

  function parseSeconds(timeTag) {
    let seconds = timeTag.split(":").reduce((acc, time) => 60 * acc + +time);
    Number(seconds);
  }
</script>

<audio 
  bind:this={audio}
  bind:currentTime={audioTime}
  preload="auto">
  <source src="{audioPath}" type="audio/mp3">
  <p>Your browser doesn't support HTML5 audio.</p>
</audio>

<button on:click={playHandler}>
  Play
</button>

<button on:click={() => {audio.pause()}}>
  Pause
</button>
