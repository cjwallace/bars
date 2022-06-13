<script lang="ts">
	export let name = 'enter a name';
	export let value = 0;
	export let width: number;
</script>

<div class="w-1/3">
	<input type="text" bind:value={name} class="w-1/2" />
	<input type="number" min="0" bind:value class="w-1/4" />
</div>
<div class="w-1/2">
	<div style="width:{50 * width}%;" class="bg-dark">&nbsp;</div>
</div>

<style lang="postcss">
	input {
		@apply inline-block border-b-darkish border-b-2 border-solid font-mono;
	}
	div {
		@apply inline-block;
	}
</style>
