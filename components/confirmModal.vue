<template>
	<div class="modalContainer">
		<p>Товар добавлен</p>
	</div>
</template>

<script>
export default {
  name: 'confirmModal',
}
</script>

<style lang="scss" scoped>
	.modalContainer {
		z-index: 100;
		position: absolute;
		top: -45px;
		font-family: 'Source Sans Pro', sans-serif;
		font-weight: 400;
		right: 40px;
		width: 200px;
		height: fit-content;
		padding: 10px 20px;
		background: #FFFEFB;
		box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
		border-radius: 10px;
		display: flex;
		justify-content: center;
		align-items: center;
	  animation-duration: 3s;
	  animation-timing-function: ease-in-out;
	  animation-name: slide;

	  @media screen and (max-width: 449px) {
	  	right: 25%;
	  }

	  @keyframes slide {
	  	0% {
	  		top: -45px;
	  	}

	  	50% {
	  		top: 30px;
	  	}

	  	100% {
	  		top: -45px;
	  	}
	  }
	}
</style>