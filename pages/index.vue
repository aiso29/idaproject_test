<template>
  <div class="pageContainer">
    <div class="pageContainer__left">
      <addProductForm class="pageContainer__form"/>
    </div>
    <div class="pageContainer__right"> 
      <div class="pageContainer__right__sortContainer">
        <div class="addButton">
          <button @click="openModal">Добавить товар</button>
        </div>
        <sortBlock />
      </div>
      <productCards class="pageContainer__cards"/>
    </div>
    <confirmModal v-if="showConfirmModal"/>
    <layoutModal v-if="showLayoutModal" />
  </div>
</template>

<script>
import addProductForm from '../components/addProductForm'
import productCards from '../components/productCards'
import sortBlock from '../components/sortBlock'
import confirmModal from '../components/confirmModal'
import layoutModal from '../components/layoutModal'

export default {
  name: 'IndexPage',

  data() {
    return {
      showConfirmModal: false,
      showLayoutModal: false
    }
  },

  created() {
    this.$root.$refs.index_component = this
  },

  methods: {
    openModal() {
      this.$root.$refs.layoutModal_component.showAddProductForm = true
      this.showLayoutModal = true
    }
  }
}
</script>

<style lang="scss">
  .pageContainer {
    display: flex;
    background: rgba(255, 254, 251, 0.8);
    width: 100%;
    height: 100vh;
    padding: 32px 24px 0 32px;
    overflow-y: scroll;

    @media screen and (max-width: 1023px) {
      padding: 32px 12px 0 16px;
    }

    &__left {
      width: 25%;
      position: sticky;
      top: 0;

      @media screen and (max-width: 999px) {
        width: 50%;
      }

      @media screen and (max-width: 449px) {
        width: 0%;
        display: none;
      }
    }

    &__right {
      width: 75%;

      @media screen and (max-width: 999px) {
        width: 50%;
      }

      @media screen and (max-width: 449px) {
        width: 100%;
      }

      &__sortContainer {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 16px;

        @media screen and (min-width: 450px) {
          justify-content: flex-end;
        }

        .addButton {
          width: fit-content;
          display: block;

          @media screen and (min-width: 450px) {
            display: none;
          }

          button {
            background: #FFFEFB;
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
            border-radius: 4px;
            height: 36px;
            border: none;
            font-family: 'Source Sans Pro', sans-serif;
            font-weight: 400;
            font-size: 12px;
            line-height: 15px;
            color: #B4B4B4;
            padding: 5px 16px;
            cursor: pointer;
            transition: all .2s ease;

            &:hover {
              color: #000;
              box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.5);
            }
          }
        }
      }
    }
  }
</style>
