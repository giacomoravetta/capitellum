<script>
	let rotationX = 0;
	let rotationY = 0;
	let isDragging = false;
	let startX = 0;
	let startY = 0;
	let cylinder;

	const letters = ['A', 'B', 'C', 'D', 'E', 'F'];

	function handleMouseDown(e) {
		isDragging = true;
		startX = e.clientX - rotationY;
		startY = e.clientY - rotationX;
	}

	function handleMouseMove(e) {
		if (!isDragging) return;

		rotationY = e.clientX - startX;
		rotationX = e.clientY - startY;

		updateTransform();
	}

	function handleMouseUp() {
		isDragging = false;
	}

	function updateTransform() {
		if (cylinder) {
			const snapAngle = 60;
			const halfSnapAngle = snapAngle / 2;

			let snappedRotation = Math.round((rotationY + halfSnapAngle) / snapAngle) * snapAngle;

			cylinder.style.transform = `rotateY(${snappedRotation}deg)`;
		}
	}

	$effect(() => {
		window.addEventListener('mousemove', handleMouseMove);
		window.addEventListener('mouseup', handleMouseUp);

		return () => {
			window.removeEventListener('mousemove', handleMouseMove);
			window.removeEventListener('mouseup', handleMouseUp);
		};
	});
</script>

<div
	class="cylinder flex items-center justify-center"
	bind:this={cylinder}
	onmousedown={handleMouseDown}
	draggable="false"
>
	{#each letters as letter, i}
		<div
			class="face relative bg-blue-900 text-white"
			style="transform: rotateY({i * 60}deg) translateZ(142px)"
		>
			{letter}
		</div>
	{/each}
</div>

<style>
	.cylinder {
		height: 100%;
		aspect-ratio: 1;
		position: relative;
		transform-style: preserve-3d;
		transition: transform 0.1s ease-out;
		cursor: grab;
	}

	.cylinder:active {
		cursor: grabbing;
	}

	.face {
		position: absolute;
		width: 100%;
		height: 100%;
		border: 1px solid white;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 48px;
		font-weight: bold;
		backface-visibility: visible;
	}
</style>
