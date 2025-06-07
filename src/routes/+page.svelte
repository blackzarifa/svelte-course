<script lang="ts">
	import { Search, AlarmCheck } from '@lucide/svelte';
	import Button from '$lib/components/Button.svelte';
	import Counter from '$lib/components/Counter.svelte';
	import DisplayName from '$lib/components/DisplayName.svelte';
	import RandomNumber from '$lib/components/RandomNumber.svelte';
	import generateNotifications from '$lib/utils/generate-notifications';
	import Notification from '$lib/components/Notification.svelte';
	import Sheet from '$lib/components/sheet/Sheet.svelte';

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
	let notifications = $state.raw(generateNotifications(3));
	let data = $state([
		[
			{ value: 'Item', bgColor: '#6aa84f', color: '#fff' },
			{ value: 'Price', bgColor: '#6aa84f', color: '#fff' },
			{ value: 'Quantity', bgColor: '#6aa84f', color: '#fff' },
			{ value: 'Total', bgColor: '#51803d', color: '#fff' }
		],
		[{ value: 'Milk' }, { value: '3' }, { value: '2' }, { value: '=MULTIPLY(B2,C2)' }],
		[{ value: 'Oats' }, { value: '4' }, { value: '1' }, { value: '=MULTIPLY(B3,C3)' }],
		[{ value: 'Honey' }, { value: '5' }, { value: '2' }, { value: '=MULTIPLY(B4,C4)' }],
		[{ value: 'Strawberries' }, { value: '2' }, { value: '2' }, { value: '=MULTIPLY(B5,C5)' }],
		[
			{ value: '', bgColor: '#b4a7d6' },
			{ value: '', bgColor: '#b4a7d6' },
			{ value: 'Total', bgColor: '#b4a7d6' },
			{ value: '=SUM(D2,D3,D4,D5)', bgColor: '#8e7eb6' }
		]
	]);

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

<div>
	<Button
		onclick={() => {
			notifications = generateNotifications(3);
		}}
	>
		Refresh
	</Button>
	<ul>
		{#each notifications as notification}
			<li>
				<Notification
					{notification}
					onremove={(id) => {
						notifications = notifications.filter((n) => n.id !== id);
					}}
				/>
			</li>
		{:else}
			<p>No notifications</p>
		{/each}
	</ul>
</div>
<hr />

<Sheet {data} />
<pre>
	{JSON.stringify(data, null, 2)}Add commentMore actions
</pre>
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

	ul {
		list-style: none;
		padding: 10px;
		margin: 0;
		li {
			margin-bottom: 10px;
		}
	}
</style>
