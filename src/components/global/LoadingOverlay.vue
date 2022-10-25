<template>
	<div class="loading-screen">
		<p>Loading data</p>
	</div>
</template>

<script>

export default {
	name: 'LoadingOverlay'
}
</script>

<style lang="scss" scoped>
	.loading-screen {
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		background: rgba(255,255,255,0.9);
		display: flex;
		align-items: center;
		justify-content: center;

		p {
			animation:spin 4s linear infinite;
		}
	}

	@keyframes spin {
		100% {
			transform:rotate(360deg);
		}
	}

</style>