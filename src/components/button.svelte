<script lang="ts">
	let clazz: string = '';
	export let disabled = false;
	export { clazz as class };
</script>

<!-- The reason we add on:click is so that you can use on:click
when using this Button component -->
<button
	on:click
	{disabled}
	class={`rounded-full p-3 text-white cursor-pointer disabled:bg-gray-500 disabled:cursor-not-allowed ${clazz}`}
>
	<slot />
</button>
