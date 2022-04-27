<script>
	let dancingMusic;

	export const start = () => {
		dancingMusic.play();
	};

	export const reset = () => {
		dancingMusic.pause();
		dancingMusic.currentTime = 0;
	};
</script>

<audio preload="auto" src="/dancing.mp3" bind:this={dancingMusic} />
