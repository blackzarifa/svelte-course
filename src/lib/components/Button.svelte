<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { HTMLButtonAttributes } from 'svelte/elements';

	type Props = HTMLButtonAttributes & {
		left?: Snippet<[boolean]>;
		right?: Snippet;
		children: Snippet<[boolean]>;
		size?: 'sm' | 'lg';
		shadow?: boolean;
		onlefthover?: () => void;
	};

	let {
		left,
		right,
		size = 'sm',
		shadow = false,
		children,
		onlefthover,
		...props
	}: Props = $props();

	let isLeftHovered = $state(false);
</script>

<button class:sm={size == 'sm'} class:lg={size == 'lg'} class:shadow {...props}>
	{#if left}
		<div
			role="presentation"
			class="left-content"
			onmouseenter={() => {
				onlefthover?.();
				isLeftHovered = true;
			}}
			onmouseleave={() => {
				isLeftHovered = false;
			}}
		>
			{@render left(isLeftHovered)}
		</div>
	{/if}

	{@render children(isLeftHovered)}

	{#if right}
		<div class="right-content">
			{@render right()}
		</div>
	{/if}
</button>

<style lang="scss">
	button {
		border: none;
		background-color: var(--buttonBgColor, #ff3e00);
		color: var(--buttonTextColor, #ffffff);
		padding: 0 20px;
		height: 45px;
		font-weight: bold;
		border-radius: 5px;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
		&:disabled {
			opacity: 0.6;
			cursor: not-allowed;
		}
		&:hover {
			background-image: linear-gradient(rgba(0, 0, 0, 0.4) 0 0);
		}
		&:active {
			background-image: linear-gradient(rgba(255, 255, 255, 0.1) 0 0);
		}
		&.sm {
			height: 45px;
		}
		&.lg {
			height: 55px;
			font-size: 20px;
		}
		&.shadow {
			box-shadow: 0 0 10px rgba(1, 1, 1, 0.3);
		}
		.left-content {
			margin-inline-end: 10px;
		}
		.right-content {
			margin-inline-start: 10px;
		}
	}
</style>
