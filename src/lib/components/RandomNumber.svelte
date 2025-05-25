<script lang="ts">
	import { onDestroy, onMount, tick, untrack } from 'svelte';

	let randomNumber = $state(Math.floor(Math.random() * 10));
	let doubleRandomNumber = $derived(randomNumber * 2);

	onMount(() => {
		console.log('the component has mounted');
		return () => {
			console.log('the component has unmounted');
		};
	});

	onDestroy(() => {
		console.log('the component is destroyed');
	});
</script>

<h2>The random number is: {randomNumber}</h2>
<h2>Double random number is: {doubleRandomNumber}</h2>
