<script lang="ts">
	import { onMount } from 'svelte';

	let count = $state(0);
	let frequency = $state(1000);
	let paused = $state(true);
	let interval: ReturnType<typeof setInterval>;

	function createInterval() {
		clearInterval(interval);
		if (paused) return;

		interval = setInterval(() => {
			count++;
		}, frequency);
	}

	function togglePlayState() {
		if (!paused) {
			paused = true;
			clearInterval(interval);
			return;
		}

		paused = false;
		createInterval();
	}

	function reset() {
		count = 0;
		createInterval();
	}

	function updateFrequency(_frequency: number) {
		frequency = _frequency;
		createInterval();
	}

	onMount(() => {
		createInterval();
		return () => {
			clearInterval(interval);
		};
	});
</script>

<h1>{count}</h1>

{frequency}
<button onclick={reset}>Reset</button>
<button onclick={togglePlayState}>{paused ? 'Play' : 'Pause'}</button>

<button
	onclick={() => {
		updateFrequency(frequency * 2);
	}}
>
	Slower
</button>
<button
	onclick={() => {
		updateFrequency(frequency / 2);
	}}
>
	Faster
</button>
