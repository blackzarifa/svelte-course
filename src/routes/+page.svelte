<script lang="ts">
	import { Search, AlarmCheck } from '@lucide/svelte';
	import Button from '$lib/components/Button.svelte';
	import Counter from '$lib/components/Counter.svelte';
	import DisplayName from '$lib/components/DisplayName.svelte';
	import RandomNumber from '$lib/components/RandomNumber.svelte';

	let html = '<p>dwdwdw</p>';
	let button: Button;

	$effect(() => {
		button.getButton().focus();
	});
</script>

<DisplayName />
<hr />

<RandomNumber />
<hr />

<Counter />
<hr />

<div class="wrapper">
	{@html html}
	<div
		role="presentation"
		onclick={(e) => {
			e.stopPropagation();
			console.log('event coming from div');
		}}
	>
		<Button
			bind:this={button}
			href={undefined}
			size="lg"
			--buttonBgColor="yellow"
			--buttonTextColor="green"
			onclick={(e) => {
				e.stopPropagation();
				console.log('event coming from button');
			}}
			onlefthover={() => {
				console.log('left hovered');
			}}
		>
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
	}
</style>
