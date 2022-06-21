<script lang="ts">
	import { maxBy } from 'lodash';

	import Bar from '$lib/components/Bar.svelte';

	type Bar = {
		name: string;
		value: number;
		width: number;
		id: number;
	};

	let id = 0;
	let bars: Bar[] = [];

	const addBar = () => {
		id = id + 1;
		bars = bars.concat({ name: 'label', value: 1, width: 1, id });
	};

	const removeBar = (id: number) => {
		bars = bars.filter((b) => b.id !== id);
	};

	$: maxValue = maxBy(bars, 'value')?.value || 1;
	$: {
		bars.forEach((bar) => (bar.width = bar.value / maxValue));
	}
</script>

<div class="title">
	<input type="text" value="TITLE" />
</div>

<div class="bars">
	{#each bars as bar}
		<button on:click={() => removeBar(bar.id)} class="remove"> - </button>
		<Bar bind:name={bar.name} bind:value={bar.value} width={bar.width} />
		<br />
	{/each}
	<button on:click={addBar} class="add">+</button>
</div>

<style lang="postcss">
	div.title {
		@apply max-w-4xl m-auto my-12 font-mono text-xl font-bold;
	}

	div.title input {
		@apply w-full;
	}

	div.bars {
		@apply max-w-4xl m-auto my-12;
	}

	button.remove {
		@apply inline-block font-mono;
	}

	button.add {
		@apply block mt-1 font-mono;
	}
</style>
