<template>
	<div class="cardsContainer">
		<productCard :card="card" v-for ="(card, index) in cards" :id="index" class="cardsContainer__card"/>
	</div>
</template>

<script>
import productCard from '../components/productCard'

import axios from 'axios';

export default {
  name: 'productCards',

  data() {
  	return {
 			cards: []
  	}
  },

  created() {
  	this.$root.$refs.productCard__component = this
  	this.fetchData()
  },

  methods: {

  	sortByPrice(param) {
  		if (param == 'asc') {
  			this.cards.sort((d1, d2) => {
  				return (d1.productPrice > d2.productPrice ? 1 : -1)
  			})
  		}
  		else {
  			this.cards.sort((d1, d2) => {
  				return (d1.productPrice < d2.productPrice ? 1 : -1)
  			})
  		}
  	},

  	sortByName() {
  		this.cards.sort((d1, d2) => {
  				return (d1.productName.toLowerCase() > d2.productName.toLowerCase() ? 1 : -1)
  			})
  	},

  	async fetchData() {
		  this.cards = JSON.parse(window.localStorage.getItem('products'))
		},

  	async saveData() {
		  const data = JSON.stringify(this.cards)
		  window.localStorage.setItem('products', data)
		},
  }
}
</script>

<style lang="scss" scoped>
	.cardsContainer {
		display: flex;
		flex-wrap: wrap;

		&__card {
			width: calc(33% - 16px);
		}
	}
</style>