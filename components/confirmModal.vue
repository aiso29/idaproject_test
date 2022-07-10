<template>
	<div class="modalContainer">
		<div class="modalContainer__window">
			<p>Товар добавлен</p>
		</div>
	</div>
</template>

<script>
export default {
  name: 'confirmModal',
}
</script>

<style lang="scss" scoped>
	.modalContainer {
		position: absolute;
		top: 0;
		right: 0;
		width: 300px;
		height: 100px;
		background: rgba(0, 0, 0, 0.4);
		display: flex;
		justify-content: center;
		align-items: center;

		&__window {
			background: #FFF;
		}
	}
</style>