<script lang="ts">
	import { Search, AlarmCheck } from '@lucide/svelte';
	import Button from '$lib/components/Button.svelte';
	import Counter from '$lib/components/Counter.svelte';
	import DisplayName from '$lib/components/DisplayName.svelte';
	import RandomNumber from '$lib/components/RandomNumber.svelte';

	let html = '<p>dwdwdw</p>';
</script>

<DisplayName />
<hr />

<RandomNumber />
<hr />

<Counter />
<hr />

<div class="wrapper">
	{@html html}
	<Button size="lg" bgColor="green" textColor="yellow">
		{#snippet left(isHovered)}
			{#if isHovered}
				<Search />
			{:else}
				<AlarmCheck />
			{/if}
		{/snippet}

		Text

		{#snippet right()}
			<AlarmCheck />
		{/snippet}
	</Button>
</div>

<style>
	:global {
		body {
			background-color: #222;
		}
	}

	.wrapper :global {
		p {
			color: white;
		}
		button {
			background-color: blue !important;
		}
	}
</style>
