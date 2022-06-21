<script lang="ts">
	export let name = 'enter a name';
	export let value = 0;
	export let width: number;
	export let destroyer: () => void;
</script>

<div class="container">
	<div class="controls">
		<div class="remove">
			<button on:click={destroyer} class="remove"> - </button>
		</div>
		<input type="text" bind:value={name} class="name" />
		<input type="number" min="0" bind:value class="value" />
	</div>
	<div class="bar-container">
		<div style="width:{100 * width}%;" class="bar">&nbsp;</div>
	</div>
</div>

<style lang="postcss">
	input {
		@apply font-mono;
		@apply outline-offset-4 outline-darkish;
	}

	input.name {
		@apply w-3/5 m-1 overflow-ellipsis;
	}

	input.value {
		@apply w-2/6 m-1 mr-2;
	}

	button.remove {
		@apply outline-darkish outline-offset-8 text-vintage-red text-xl;
	}

	div {
		@apply inline-block;
	}

	div.container {
		@apply flex border rounded-md border-transparent p-4;
		/* @apply hover:border hover:border-gray-400; */
	}

	div.remove {
		@apply w-1/6;
	}

	div.controls {
		@apply flex w-1/3;
	}

	div.bar-container {
		@apply w-2/3;
	}

	div.bar {
		@apply bg-dark pt-1 rounded-sm;
	}
</style>
