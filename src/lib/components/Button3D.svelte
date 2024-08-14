<script>
	import { T } from '@threlte/core';
	import { HTML } from '@threlte/extras';
	import { spring } from 'svelte/motion';
	import { Vector3 } from 'three';

	export let position = new Vector3();

	let isHovering = false;
	let isPointerDown = false;

	let buttonScale = spring(0);
	$: buttonScale.set(isPointerDown ? 3 : isHovering ? 4 : 2, {
		hard: isPointerDown
	});
</script>

<T.Group position.x={position.x} position.y={position.y} position.z={position.z} lookAt={[0, 0, 0]}>
	<HTML rotation.y={Math.PI} scale={$buttonScale} transform occlude>
		<button
			on:pointerenter={() => (isHovering = true)}
			on:pointerleave={() => {
				isPointerDown = false;
				isHovering = false;
			}}
			on:pointerdown={() => (isPointerDown = true)}
			on:pointerup={() => (isPointerDown = false)}
			on:pointercancel={() => {
				isPointerDown = false;
				isHovering = false;
			}}
			on:click={() => console.log('clicked')}
		>
			<slot />
		</button>
	</HTML>
</T.Group>
