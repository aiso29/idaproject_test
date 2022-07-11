<template>
	<div class="card">
		<div class="card__delete" @click="deleteProduct(id)">
			<img src="~/assets/img/deleteIcon.png">
		</div>
		<div class="card__img">
			<img :src="card.productPhotoLink" alt="">
		</div>
		<div class="card__text">
			<div class="card__text__title">
				<h1>{{card.productName}}</h1>
			</div>
			<div class="card__text__description">
				<p>{{card.productDescription.length > 120 ? card.productDescription.slice(0, 120) + '...' : card.productDescription}}</p>
			</div>
			<div class="card__text__price">
				<p>{{card.productPrice.toString().replace(/(\d)(?=(\d{3})+$)/g, '$1 ')}} руб.</p>
			</div>
		</div>
	</div>
</template>

<script>
export default {
  name: 'productCard',

  props: {
  	card: {
  		type: Object,
  		default() {
  			return {}
  		}
  	},

  	id: {
  		type: Number,
  		default: null
  	}
  },

  methods: {
  	deleteProduct(id) {
  		this.$root.$refs.productCard__component.cards.splice(id, 1)
  		this.$root.$refs.productCard__component.saveData()
  	}
  }
}
</script>

<style lang="scss" scoped>
	.card {
		position: relative;
		background: #FFFEFB;
		box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
		border-radius: 4px;
		height: 423px;
		cursor: pointer;
		margin: 0 8px 16px 8px;
		transition: all .2s ease;

		&:hover &__delete {
			display: flex;
		}

		&:hover {
			transform: scale(1.05);
		}

		&__delete {
			position: absolute;
			right: -8px;
			top: -8px;
			display: none;
			background: #FF8484;
			box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
			border-radius: 10px;
			width: 32px;
			height: 32px;
			align-items: center;
			justify-content: center;

			img {
				width: 16px;
				height: 16px;
			}
		}
		
		&__img {

			img {
				height: 200px;
				width: 100%;
				object-fit: cover;
				border-radius: 4px 4px 0 0;
			}
		}

		&__text {
			padding: 16px 16px 24px 16px;

			&__title {
				margin-bottom: 16px;

				h1 {
					font-family: 'Source Sans Pro', sans-serif;
					font-weight: 600;
					font-size: 20px;
					line-height: 25px;
					color: #3F3F3F;

					@media screen and (max-width: 649px) {
						font-size: 16px;
						line-height: 21px;
					}
				}
			}

			&__description {
				margin-bottom: 32px;

				p {
					font-family: 'Source Sans Pro', sans-serif;
					font-weight: 400;
					font-size: 16px;
					line-height: 20px;
					color: #3F3F3F;
					text-align: justify;

					@media screen and (max-width: 649px) {
						font-size: 13px;
						line-height: 17px;
					}
				}
			}

			&__price {

				p {
					font-family: 'Source Sans Pro', sans-serif;
					font-weight: 600;
					font-size: 24px;
					line-height: 30px;
					color: #3F3F3F;

					@media screen and (max-width: 649px) {
						font-size: 20px;
						line-height: 26px;
					}
				}
			}
		}
	}
</style>