<script lang="ts">
	import { flip } from 'svelte/animate';
	import maxBy from 'lodash/maxBy';

	import Bar from '$lib/components/Bar.svelte';

	type Bar = {
		name: string;
		value: number;
		width: number;
		id: number;
	};

	let id = 0;
	const defaultBar = { name: 'label', value: 1, width: 1, id };
	let bars: Bar[] = [defaultBar];

	const addBar = () => {
		id = id + 1;
		bars = bars.concat({ name: 'label', value: 1, width: 1, id });
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
	<input type="text" value="TITLE" />
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
		@apply max-w-4xl m-auto my-12 font-mono text-xl font-bold;
	}

	div.title input {
		@apply w-full outline-darkish p-2;
	}

	div.bars {
		@apply max-w-4xl m-auto my-12;
	}

	button.add {
		@apply block mt-1 ml-4 font-mono text-xl outline-darkish outline-offset-8;
	}
</style>
