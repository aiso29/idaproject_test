<template>
	<div class="container">
		<div class="container__header" v-if="!modal">
			<h1 class="container__header__title">Добавление товара</h1>
		</div>
		<div class="container__main">
			<div class="container__main__title" v-if="modal">
				<h1>Добавление товара</h1>
				<div class="cross" @click="closeModal"></div>
			</div>
			<div class="container__main__row">
				<label for="productName">
					<p>Наименование товара<span>*</span></p>
				</label>
				<input type="text" name="productName" :class="{invalid: isInvalidProductName}" placeholder="Введите наименование товара" v-model.trim="productName"/>
				<p class="invalidText" v-if="isInvalidProductName">Поле является обязательным</p>
			</div>
			<div class="container__main__row">
				<label for="productDescription">
					<p>Описание товара</p>
				</label>
				<textarea name="productDescription" v-model.trim="productDescription" placeholder="Введите описание товара"></textarea>
			</div>
			<div class="container__main__row">
				<label for="productPhotoLink">
					<p>Ссылка на изображение товара<span>*</span></p>
				</label>
				<input type="text" v-model.trim="productPhotoLink" :class="{invalid: isInvalidProductPhotoLink}" name="productPhotoLink" placeholder="Введите ссылку" />
				<p class="invalidText" v-if="isInvalidProductPhotoLink">Поле является обязательным</p>
			</div>
			<div class="container__main__row">
				<label for="productPrice">
					<p>Цена товара<span>*</span></p>
				</label>
				<input type="text" @input="formatToPrice(productPrice)" v-model.trim="productPrice" :class="{invalid: isInvalidProductPrice}" name="productPrice" placeholder="Введите цену" />
				<p class="invalidText" v-if="isInvalidProductPrice">Поле является обязательным</p>
			</div>
			<div class="container__main__row">
				<button @click="addProduct()">Добавить товар</button>
			</div>
		</div>
	</div>
</template>

<script>
export default {
  name: 'addProductForm',

  data() {
  	return {
  		productName: '',
  		productDescription: '',
  		productPhotoLink: '',
  		productPrice: '',
  		isInvalidProductName: false,
  		isInvalidProductPhotoLink: false,
  		isInvalidProductPrice: false,
  	}
  },

  props: {
  	modal: {
  		type: Boolean,
  		default: false
  	}
  },

  methods: {
  	closeModal() {
  		this.$emit('close')
  	},

  	addProduct() {
  		if (this.validate()) {
  			let card = {
  				productName: this.productName,
  				productDescription: this.productDescription,
  				productPhotoLink: this.productPhotoLink,
  				productPrice: this.productPrice
  			}
  			this.$root.$refs.productCard__component.cards.push(card)
  			this.$root.$refs.productCard__component.saveData()
			  this.$root.$refs.index_component.showConfirmModal = true
			  setTimeout(() => {
			  	this.$root.$refs.index_component.showConfirmModal = false
			  }, 3000)
  		}
  	},

  	formatToPrice(price) {
  		if (!Number(this.productPrice)) {
  			this.productPrice = price.slice(0, this.productPrice.length - 1)
  		}
  	},

  	validate() {
  		let flag = true
  		if (this.productName === '') {
  			this.isInvalidProductName = true
  			flag = false
  		}
  		else {
  			this.isInvalidProductName = false
  		}
  		if (this.productPhotoLink === '') {
  			this.isInvalidProductPhotoLink = true
  			flag = false
  		}
  		else {
  			this.isInvalidProductPhotoLink = false
  		}
  		if (this.productPrice === '') {
  			this.isInvalidProductPrice = true
  			flag = false
  		}
  		else {
  			this.isInvalidProductPrice = false
  		}
  		return flag
  	}
  }
}
</script>

<style lang="scss" scoped>
	.container {
		width: 100%;
		margin-right: 8px;

		@media screen and (max-width: 449px) {
			margin: 0;
		}

		&__header {

			&__title{
				font-family: 'Source Sans Pro', sans-serif;
				font-weight: 600;
				font-size: 28px;
				line-height: 35px;
				color: rgba(63, 63, 63, 1);

				@media screen and (max-width: 1199px) {
					font-size: 23px;
					line-height: 30px;
				}

				@media screen and (max-width: 767px) {
					font-size: 20px;
					line-height: 27px;
				}
			}
		}

		&__main {
			width: 100%;
			background: #FFFEFB;
			box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
			border-radius: 4px;
			padding: 24px;

			&__title {
				margin-bottom: 20px;
				display: flex;
				justify-content: space-between;
				align-items: center;

				h1 {
					font-family: 'Source Sans Pro', sans-serif;
					font-weight: 600;
					font-size: 20px;
					line-height: 27px;
					color: rgba(63, 63, 63, 1);
				}

				.cross {
					position: relative;
					width: 20px;
					height: 20px;
					border: 1px solid #000;
					border-radius: 10px;
					cursor: pointer;
					transition: all .2s ease;

					&:after, &:before {
						content: '';
						width: 1px;
						height: 10px;
						background: #000;
						position: absolute;
					}

					&:after {
						top: calc(50% - 5px);
						left: calc(50% - 1px);
						transform: rotate(45deg);
					}

					&:before {
						top: calc(50% - 5px);
						left: calc(50% - 1px);
						transform: rotate(-45deg);
					}

					&:hover {
						transform: scale(1.1);
					}
				}
			}

			&__row {
				margin-bottom: 16px;

				.invalidText {
					font-family: 'Source Sans Pro', sans-serif;
					font-weight: 400;
					font-size: 8px;
					line-height: 10px;
					color: #FF8484;
					margin-top: 4px;
				}

				p {
					font-family: 'Source Sans Pro', sans-serif;
					font-weight: 400;
					font-size: 10px;
					line-height: 13px;
					color: #49485E;
					margin-bottom: 4px;

					span {
						color: #FF8484;
					}
				}

				.invalid {
					border: 1px solid #FF8484;
				}

				input {
					font-family: 'Source Sans Pro', sans-serif;
					font-weight: 400;
					font-size: 12px;
					line-height: 15px;
					color: #3F3F3F;
					width: 100%;
					background: #FFFEFB;
					box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
					border-radius: 4px;
					height: 36px;
					border-width: 0;
					padding: 10px 16px;

					&::placeholder {
						color: #B4B4B4;
					}
				}

				textarea {
					font-family: 'Source Sans Pro', sans-serif;
					font-weight: 400;
					font-size: 12px;
					line-height: 15px;
					color: #3F3F3F;
					resize: none;
					width: 100%;
					height: 108px;
					background: #FFFEFB;
					box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
					border-radius: 4px;
					border-width: 0;
					padding: 10px 16px;

					&::placeholder {
						color: #B4B4B4;
					}
				}

				button {
					width: 100%;
					height: 36px;
					background: #EEEEEE;
					border-radius: 10px;
					border-width: 0;
					color: #B4B4B4;
					font-family: 'Inter', sans-serif;
					font-weight: 600;
					font-size: 12px;
					line-height: 15px;
					cursor: pointer;
					transition: all .2s ease;

					&:hover {
						background: rgba(123, 174, 115, 1);
						color: #FFFFFF;
					}
				}
			}
		}
	}
</style>