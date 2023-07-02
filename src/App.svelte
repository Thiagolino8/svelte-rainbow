<script lang="ts">
	import rainbowGradient from 'rainbow-gradient'

	const rainbowColors = rainbowGradient(360).map(([r, g, b]) => `rgb(${r},${g},${b})`)
	let colors = new Array(360 * 4).fill(0).map((_, i) => rainbowColors[i % rainbowColors.length])
	const length = colors.length;

	(function update() {
		colors.push(colors.shift())
		colors = colors
		requestAnimationFrame(update)
	})()
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