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
<Button>
	{#snippet left()}
		<Search />
	{/snippet}
	Text
	{#snippet right()}
		<AlarmCheck />
	{/snippet}
</Button>
