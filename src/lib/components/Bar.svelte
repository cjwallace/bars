<script lang="ts">
	export let name = 'enter a name';
	export let value = 0;
	export let width: number;
</script>

<div class="container">
	<div class="controls container">
		<input type="text" bind:value={name} class="name" />
		<input type="number" min="0" bind:value class="value" />
	</div>
	<div class="bar-container">
		<div style="width:{100 * width}%;" class="bar">&nbsp;</div>
	</div>
</div>

<style lang="postcss">
	input {
		@apply hover:border-b-2 border-b-darkish border-solid font-mono;
	}

	input.name {
		@apply w-1/2;
	}

	input.value {
		@apply w-1/4;
	}

	div {
		@apply inline-block;
	}

	div.container {
		@apply flex;
	}

	div.controls {
		@apply w-1/3;
	}

	div.bar-container {
		@apply w-2/3;
	}

	div.bar {
		@apply bg-dark;
	}
</style>
