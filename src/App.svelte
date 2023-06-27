<script lang="ts">
	import rainbowGradient from 'rainbow-gradient'
	import { onMount } from 'svelte'

	const rainbowColors = rainbowGradient(360).map(([r, g, b]: number[]) => `rgb(${r},${g},${b})`)
	let colors = new Array(360 * 4).fill(0).map((_, i) => rainbowColors[i % rainbowColors.length])

	const update = () => {
		colors.push(colors.shift() as string)
		colors = colors
		requestAnimationFrame(update)
	}

	onMount(() => {
		requestAnimationFrame(update)
	})

	const length = colors.length
</script>

<main
	style="display: grid;
		grid-template-columns: repeat({length}, 1fr);
    height: 100vh;
    width: 100vw;"
>
	{#each colors as color}
		<div style="background-color: {color};" />
	{/each}
</main>
