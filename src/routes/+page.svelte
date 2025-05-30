<script lang="ts">
	import { Search, AlarmCheck } from '@lucide/svelte';
	import Button from '$lib/components/Button.svelte';
	import Counter from '$lib/components/Counter.svelte';
	import DisplayName from '$lib/components/DisplayName.svelte';
	import RandomNumber from '$lib/components/RandomNumber.svelte';
</script>

<DisplayName />
<hr />
<RandomNumber />
<hr />
<Counter />
<hr />
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
