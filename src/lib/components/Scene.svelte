<script lang="ts">
	import { T } from '@threlte/core';
	import {
		ContactShadows,
		Float,
		Grid,
		MeshLineGeometry,
		MeshLineMaterial,
		OrbitControls
	} from '@threlte/extras';
	import { IcosahedronGeometry, Vector3 } from 'three';

	const geometry = new IcosahedronGeometry(10, 3);
</script>

<T.OrthographicCamera makeDefault position={[-10, -10, 10]} zoom={29}>
	<OrbitControls
		lookAt={[0, 10, 0]}
		autoRotate
		enableDamping
		autoRotateSpeed={3.5}
		target.y={1.5}
		minPolarAngle={1.2}
		maxPolarAngle={3}
		maxZoom={30}
		minZoom={20}
	/>
</T.OrthographicCamera>

<T.DirectionalLight intensity={1} position.x={-5} position.y={5} color="#FFAD00" />
<T.DirectionalLight intensity={1} position.x={5} position.y={10} color="#FFAD00" />
<T.DirectionalLight intensity={1} position.z={-5} position.y={-5} color="#F63E44" />
<T.DirectionalLight intensity={1} position.z={5} position.y={-5} color="#F63E44" />
<T.DirectionalLight intensity={1} position.x={-5} position.y={-10} color="#F63E44" />
<T.AmbientLight intensity={0.2} />

<ContactShadows scale={10} blur={2} far={2.5} opacity={0.5} />

<Float floatIntensity={1} floatingRange={[-5, 5]}>
	<Grid
		position.y={100}
		cellColor="#ffffff"
		sectionColor="#ffffff"
		sectionThickness={0}
		cellSize={1}
		fadeDistance={10}
		type="polar"
	/>

	<T.Mesh scale={[0.99, 0.99, 0.99]} {geometry} position={[0, 0, 0]} rotation={[-5, 128, 10]}>
		<T.MeshPhongMaterial shininess={100} color="silver" flatShading />
	</T.Mesh>

	<T.Mesh {geometry} position={[0, 0, 0]} rotation={[-5, 128, 10]}>
		<T.MeshStandardMaterial wireframe />
	</T.Mesh>

	<T.Mesh>
		<MeshLineGeometry points={[new Vector3(0, 0, 0), new Vector3(0, 100, 0)]} />
		<MeshLineMaterial width={0.005} color="#F63E44" />
	</T.Mesh>
</Float>
