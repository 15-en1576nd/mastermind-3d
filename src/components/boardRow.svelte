<script lang="ts">
	import emojiMap from '$lib/emojimap';
	import EmojiSlot from './emojiSlot.svelte';
	import Emoji from './emoji.svelte';
	import { game, selectedEmoji } from '$lib/stores';
	import SidebarHints from './sidebarHints.svelte';

	export let rowIndex: number;
	export let disabled: boolean;
</script>

<div style={`grid-template-columns: repeat(${$game.code.length + 1}, 1fr);`}>
	{#each $game.rows[rowIndex].code as column, columnIndex}
		<button
			{disabled}
			on:click={() => {
				if (disabled) return;
				game.update((cgame) => {
					//@ts-ignore
					cgame.rows[rowIndex].code[columnIndex] = $selectedEmoji;
					return cgame;
				});
			}}
		>
			<EmojiSlot active={$game.maxGuesses - $game.guessCount - 1 === rowIndex}>
				{#if column !== 8}
					<Emoji emoji={emojiMap[column]} />
				{/if}
			</EmojiSlot>
		</button>
	{/each}
	<SidebarHints hints={$game.rows[rowIndex].hints} />
</div>

<style>
	div {
		display: grid;
		grid-gap: 0.5rem;
		max-width: min-content;
		margin-left: auto;
		margin-right: auto;
	}
</style>
