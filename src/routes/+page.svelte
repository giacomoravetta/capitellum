<script>
	import PentagramFace from '../components/pentagramFace.svelte';
</script>

<div class="page flex h-dvh w-dvw items-center justify-center bg-blue-900">
	<div
		class="main gap- justify-cente flex h-[80%] w-[80%] flex-col items-center gap-5"
		draggable="false"
	>
		<PentagramFace />
		<PentagramFace />
		<PentagramFace />
		<PentagramFace />
		<PentagramFace />
	</div>
</div>

<style>
	.main {
		-webkit-user-select: none;
		-ms-user-select: none;
		user-select: none;
		transform-style: preserve-3d;
		transform: rotateX(-10deg);
	}
</style>
