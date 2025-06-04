<script lang="ts">
	import { Search, AlarmCheck } from '@lucide/svelte';
	import Button from '$lib/components/Button.svelte';
	import Counter from '$lib/components/Counter.svelte';
	import DisplayName from '$lib/components/DisplayName.svelte';
	import RandomNumber from '$lib/components/RandomNumber.svelte';
	import generateNotifications from '$lib/utils/generate-notifications';

	let html = '<p>dwdwdw</p>';
	let button: Button;

	let array = $state([1, 2, 3, 4]);
	let object = $state({
		firstName: 'Ali',
		lastName: 'Alaa',
		address: {
			city: 'City',
			street: 'Street'
		}
	});
	let notifications = $state(generateNotifications());

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
<hr />

<div>
	<h2>{object.firstName}</h2>
	Add commentMore actions
	<h2>{object.address.city}</h2>

	<input bind:value={object.firstName} />
	<input bind:value={object.address.city} />
	<input bind:value={object.address.street} />
	<p>{array}</p>
	<button
		onclick={() => {
			array[1] = Math.random() * 10;
		}}
	>
		Add to array
	</button>
	<button
		onclick={() => {
			console.log($state.snapshot(object));
		}}
	>
		Log Snapshot
	</button>
</div>
<hr />

<ul>
	{#each notifications as { title, body, date }}
		{@const dateObject = new Date(date)}
		<li>
			<h5>{title}</h5>
			<p>{body}</p>
			<time datetime={dateObject.toISOString()}>{dateObject.toLocaleDateString()}</time>
		</li>
	{:else}
		<p>No notifications</p>
	{/each}
</ul>
<hr />

<style>
	:global {
		body {
			background-color: #222;
			color: #fff;
		}
	}

	.wrapper :global {
		p {
			color: white;
		}
	}
</style>
