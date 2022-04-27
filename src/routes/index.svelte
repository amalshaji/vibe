<script>
	import { draggable } from '@neodrag/svelte';
	import PlayBtn from '$lib/components/PlayBtn.svelte';
	import Music from '$lib/components/Music.svelte';

	let play = false;
	let partner = false;
	let dancingMusic;
	let i = 0;
	let partnerImage = '/doge-flip.gif';

	const delay = (delayInms) => {
		return new Promise((resolve) => {
			setTimeout(() => {
				resolve(2);
			}, delayInms);
		});
	};

	const startDancing = () => {
		dancingMusic.start();
		setTimeout(() => {
			play = true;
		}, 1500);

		setTimeout(async () => {
			partner = true;
			while (play && i < 70) {
				if (i % 4 == 0) {
					partnerImage = partnerImage == '/doge.gif' ? '/doge-flip.gif' : '/doge.gif';
					party.confetti(document.getElementById('podium'), {
						shapes: ['square', 'circle', 'roundedRectangle']
					});
				}
				i++;
				await delay(250);
			}
			partner = false;
		}, 17500);

		setTimeout(() => {
			dancingMusic.reset();
			play = false;
			i = 0;
		}, 36000);
	};
</script>

<svelte:head>
	<title>Vibe</title>
	<link rel="preload" as="image" href="/doge.gif" />
	<link rel="preload" as="image" href="/doge-flip.gif" />
	<script defer src="/party.min.js"></script>
</svelte:head>

<Music bind:this={dancingMusic} />

<div class="grid place-items-center h-screen bg-gray-900" id="podium">
	{#if play}
		<div class="flex">
			<div use:draggable class="mx-2">
				<img src="/dancing.gif" alt="dancing doge" />
			</div>
			{#if partner}
				<div use:draggable>
					<img src={partnerImage} alt="dancing partner" />
				</div>
			{/if}
		</div>
	{:else}
		<PlayBtn on:play={startDancing} />
	{/if}
</div>
