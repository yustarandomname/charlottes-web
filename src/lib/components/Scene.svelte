<script lang="ts">
	import { T, useLoader } from '@threlte/core';
	import {
		ContactShadows,
		Grid,
		MeshLineGeometry,
		MeshLineMaterial,
		OrbitControls
	} from '@threlte/extras';
	import { Vector3 } from 'three';
	import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
	import Button3D from './Button3D.svelte';
	import { injectLookAtPlugin } from './lookAtPlugin';

	export let ambientFactor = 3;

	const gltf = useLoader(GLTFLoader).load('/disco ball.glb');

	injectLookAtPlugin();
</script>

<T.OrthographicCamera makeDefault position={[-10, -10, 10]} zoom={29}>
	<OrbitControls
		lookAt={[0, 10, 0]}
		autoRotate
		enableDamping
		autoRotateSpeed={1.5}
		enablePan={false}
		target.y={1.5}
		minPolarAngle={1.2}
		maxPolarAngle={3}
		maxZoom={30}
		minZoom={20}
	/>
</T.OrthographicCamera>

<T.DirectionalLight intensity={30} position.x={-50} position.y={50} color="#FFAD00" />
<T.DirectionalLight
	intensity={30}
	position.x={-50}
	position.y={-50}
	position.z={50}
	color="#F63E44"
/>
<T.DirectionalLight intensity={30} position.x={50} position.y={50} color="#FFAD00" />
<T.DirectionalLight
	intensity={30}
	position.x={50}
	position.y={-50}
	position.z={-50}
	color="#F63E44"
/>
<T.AmbientLight intensity={ambientFactor} color="#7e22ce" />

<ContactShadows scale={10} blur={2} far={2.5} opacity={0.5} />

<Grid
	position.y={100}
	cellColor="#ffffff"
	sectionColor="#ffffff"
	sectionThickness={0}
	cellSize={1}
	fadeDistance={10}
	type="polar"
/>

<T.Group scale={12}>
	{#if $gltf}
		<T is={$gltf.scene} scale={0.99}></T>
	{/if}
</T.Group>

<T.Mesh>
	<MeshLineGeometry points={[new Vector3(0, 0, 0), new Vector3(0, 100, 0)]} />
	<MeshLineMaterial width={0.005} color="#F63E44" />
</T.Mesh>

<Button3D position={new Vector3(15, 5, 0)}>Contact</Button3D>
<Button3D position={new Vector3(-15, -5, 0)}>Contact</Button3D>
<Button3D position={new Vector3(0, 5, 15)}>DJ</Button3D>
<Button3D position={new Vector3(0, -5, -15)}>DJ</Button3D>
