<script lang="ts">
	import { flip } from 'svelte/animate';
	import { maxBy } from 'lodash-es';

	import Bar from '$lib/components/Bar.svelte';

	type Bar = {
		name: string;
		value: number;
		width: number;
		id: number;
	};

	let id = 0;
	const defaultBar = (id: number): Bar => ({ name: 'Edit me', value: 1, width: 1, id });
	let bars: Bar[] = [defaultBar(id)];

	const addBar = () => {
		id = id + 1;
		bars = bars.concat(defaultBar(id));
	};

	const removeBar = (id: number) => {
		bars = bars.filter((b) => b.id !== id);
	};

	const addButton = Symbol('addButton');

	$: maxValue = maxBy(bars, 'value')?.value || 1;
	$: {
		bars.forEach((bar) => (bar.width = bar.value / maxValue));
	}

	let displayBars: Array<Bar | typeof addButton>;
	$: displayBars = [...bars, addButton];
</script>

<div class="title">
	<input type="text" value="THIS IS A FANTASTIC, AND ✨ EDITABLE ✨, TITLE FOR A BAR CHART" />
</div>

<div class="bars">
	{#each displayBars as bar (bar)}
		<div animate:flip={{ duration: 200 }}>
			{#if bar == addButton}
				<button on:click={addBar} class="add">+</button>
			{:else}
				<Bar
					bind:name={bar.name}
					bind:value={bar.value}
					width={bar.width}
					destroyer={() => removeBar(bar.id)}
				/>
				<br />
			{/if}
		</div>
	{/each}
</div>

<style lang="postcss">
	div.title {
		@apply max-w-4xl m-auto my-12 p-2;
	}

	input {
		@apply text-center overflow-ellipsis text-xl font-bold font-mono;
	}

	div.title input {
		@apply w-full outline-darkish p-2;
	}

	div.bars {
		@apply max-w-4xl m-auto my-12;
	}

	button.add {
		@apply block mt-1 outline-darkish outline-offset-8 text-xl font-extrabold;
	}
</style>
