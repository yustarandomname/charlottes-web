<script lang="ts">
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';

	let ambientFactor = 3;
</script>

<div style="display: flex; position: absolute; top: 1rem; left: 1rem; z-index: 10;">
	<input type="range" bind:value={ambientFactor} />
	<span style="margin-left: 1rem">{ambientFactor}</span>
</div>

<Canvas>
	<Scene {ambientFactor} />
</Canvas>
