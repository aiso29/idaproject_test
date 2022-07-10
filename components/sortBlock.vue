<template>
	<div class="sortContainer" @click="showSortOptions = !showSortOptions">
   	<p class="sortChoosen">{{choosenOption}}</p>
     <div class="sortContainer__options" v-if="showSortOptions">
       <p class="option" v-for="option in options" @click="chooseOption(option)">{{option.type}}</p>
      </div>
  </div>
</template>

<script>
export default {
  name: 'sortBlock',

  data() {
  	return {
  		showSortOptions: false,
  		choosenOption: 'По умолчанию',
  		options: [
  			{
  				id: 1,
	  			type: 'По умолчанию'
	  		},
	  		{
	  			id: 2,
	  			type: 'По цене min'
	  		},
	  		{
	  			id: 3,
	  			type: 'По цене max'
	  		},
	  		{
	  			id: 4,
	  			type: 'По названию'
	  		}
  		]
  	}
  },

  methods: {
  	chooseOption(option) {
  		this.choosenOption = option.type
  		switch(option.id) {
  			case 1:
  				this.$root.$refs.productCard__component.fetchData()
  				break
  			case 2:
  				this.$root.$refs.productCard__component.sortByPrice('asc')
  				break
  			case 3:
  				this.$root.$refs.productCard__component.sortByPrice('desc')
  				break
  			case 4:
  				this.$root.$refs.productCard__component.sortByName()
  				break
  		}
  	}
  }
}
</script>

<style lang="scss" scoped>
	.sortContainer {
		width: fit-content;
    background: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    height: 36px;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px 26px 10px 16px;
    cursor: pointer;
    position: relative;
    min-width: 120px;

    &__options {
	    position: absolute;
	    top: 36px;
	    left: 0;
	    width: 100%;
	    background: #FFFEFB;
	    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
	    border-radius: 4px;
	    padding: 10px 0;
	    z-index: 10;
	  }

    .option {
      font-family: 'Source Sans Pro', sans-serif;
      font-weight: 400;
      font-size: 12px;
      line-height: 15px;
      color: #B4B4B4;
      padding: 5px 16px;

      &:hover {
        background: #edecea;
      }
    }

    .sortChoosen {
      font-family: 'Source Sans Pro', sans-serif;
      font-weight: 400;
      font-size: 12px;
      line-height: 15px;
      color: #B4B4B4;
      margin: 0;

      &::after, &:before {
        content: '';
        position: absolute;
        width: 1px;
        background: #B4B4B4;
        height: 6px;
        top: calc(50% - 2px);
        right: 10px;
        transform: rotate(45deg);
      }

      &::after {
        right: 10px;
        transform: rotate(45deg);
      }

      &::before {
        right: 14px;
        transform: rotate(-45deg);
      }
    }
	}
</style>