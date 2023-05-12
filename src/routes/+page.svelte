<script>
	import { Canvas } from '@threlte/core';
	import Scene from '$lib/Scene.svelte';

	let width = window.innerWidth;
	let height = window.innerHeight;
</script>

<svelte:window
	on:resize={() => {
		width = window.innerWidth;
		height = window.innerHeight;
	}}
/>

<Canvas size={{ width, height }}><Scene /></Canvas>
