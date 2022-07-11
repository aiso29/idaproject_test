<template>
	<div class="layoutContainer">
		<addProductForm :modal="true" @close="closeAddProductForm"/>
	</div>
</template>

<script>
import addProductForm from '../components/addProductForm'

export default {
  name: 'layoutModal',

  created() {
  	this.$root.$refs.layoutModal_component = this
  },

  methods: {
  	closeAddProductForm() {
  		this.$root.$refs.index_component.showLayoutModal = false
  	}
  }
}
</script>

<style lang="scss" scoped>
	.layoutContainer {
		width: 100%;
		height: 100vh;
		background: rgba(0, 0, 0, 0.4);
		position: absolute;
		top: 0;
		left: 0;
		display: flex;
		justify-content: center;
		align-items: center;
	}
</style>