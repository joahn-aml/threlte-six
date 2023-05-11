<script>
	import { T, useFrame } from '@threlte/core';
	import { interactivity, OrbitControls } from '@threlte/extras';
	import { spring } from 'svelte/motion';
	import { get } from 'svelte/store';

	interactivity();
	const scale = spring(1);

	let rotation = 0;
	const rotationSpeed = spring(0, {
		stiffness: 0.01,
		damping: 1
	});
	useFrame((_state, delta) => {
		rotation += get(rotationSpeed) * delta;
	});
</script>

<T.PerspectiveCamera
	makeDefault
	position={[10, 10, 10]}
	on:create={({ ref }) => {
		ref.lookAt(0, 1, 0);
	}}
>
	<OrbitControls enableDamping />
</T.PerspectiveCamera>

<T.DirectionalLight position={[3, 10, 7]} />
<T.AmbientLight intensity={0.1} />

<T.Mesh
	rotation.y={rotation}
	position.y={1}
	scale={$scale}
	on:pointerenter={() => {
		scale.set(1.1);
		rotationSpeed.set(0);
	}}
	on:pointerleave={() => scale.set(1)}
	on:click={() => rotationSpeed.set(1)}
>
	<T.BoxGeometry args={[1, 2, 1]} />
	<T.MeshStandardMaterial color="aquamarine" />
</T.Mesh>
