<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	const startPlay = () => {
		dispatch('play');
	};
</script>

<button
	on:click={startPlay}
	class="py-2.5 flex px-5 mr-2 mb-2 text-sm font-medium text-gray-900 focus:outline-none bg-white rounded-lg border border-gray-200 hover:text-blue-700 focus:z-10 focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-700"
>
	<div class="svg-wrapper-1">
		<div class="svg-wrapper">
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
				<path fill="none" d="M0 0h24v24H0z" />
				<path
					fill="currentColor"
					d="M1.946 9.315c-.522-.174-.527-.455.01-.634l19.087-6.362c.529-.176.832.12.684.638l-5.454 19.086c-.15.529-.455.547-.679.045L12 14l6-8-8 6-8.054-2.685z"
				/>
			</svg>
		</div>
	</div>
	<span>Vibe</span>
</button>

<style>
	/* From uiverse.io by @adamgiebl */
	button {
		font-family: inherit;
		font-size: 20px;
		display: flex;
		align-items: center;
		border-radius: 16px;
		overflow: hidden;
		transition: all 0.2s;
	}

	button span {
		display: block;
		margin-left: 0.3em;
		transition: all 0.3s ease-in-out;
	}

	button svg {
		display: block;
		transform-origin: center center;
		transition: transform 0.3s ease-in-out;
	}

	button:hover .svg-wrapper {
		animation: fly-1 0.6s ease-in-out infinite alternate;
	}

	button:hover svg {
		transform: translateX(1.2em) rotate(45deg) scale(1.1);
	}

	button:hover span {
		transform: translateX(5em);
	}

	button:active {
		transform: scale(0.95);
	}

	@keyframes fly-1 {
		from {
			transform: translateY(0.1em);
		}

		to {
			transform: translateY(-0.1em);
		}
	}
</style>
