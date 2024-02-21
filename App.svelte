<script>
	export let name;

  let videoElement;
  let isPlaying = false;
  let currentTime = 0;
  let duration = 0;

  function togglePlay() {
    if (videoElement.paused) {
      videoElement.play();
      isPlaying = true;
    } else {
      videoElement.pause();
      isPlaying = false;
    }
  }

  function stop() {
    videoElement.pause();
    videoElement.currentTime = 0;
    isPlaying = false;
    currentTime = 0;
  }

  function updateTime() {
    currentTime = videoElement.currentTime;
  }

  function seek(e) {
    const seekTime = e.target.value;
    videoElement.currentTime = seekTime;
    currentTime = seekTime;
  }

  function loadedMetadata() {
    duration = videoElement.duration;
  }
</script>
<video
  bind:this={videoElement}
  src="your-video.mp4"
  on:timeupdate={updateTime}
  on:loadedmetadata={loadedMetadata}
></video>

<div>
  <button on:click={togglePlay}>
    {isPlaying ? "Pause" : "Play"}
  </button>
  <button on:click={stop}>Stop</button>
  <input
    type="range"
    min="0"
    max={duration}
    step="1"
    bind:value={currentTime}
    on:input={seek}
  />
</div>

<main>
	
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<style>
  button {
    margin-right: 10px;
  }
</style>