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

<div class="max-w-xl m-auto my-12 font-mono text-xl font-bold">
	<input type="text" value="TITLE" class="w-full" />
</div>

<div class="max-w-xl m-auto my-12">
	{#each bars as bar}
		<button on:click={() => removeBar(bar.id)} class="inline-block font-mono"> - </button>
		<Bar bind:name={bar.name} bind:value={bar.value} width={bar.width} />
		<br />
	{/each}
	<button on:click={addBar} class="block mt-1 font-mono">+</button>
</div>
