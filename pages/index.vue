<template>
  <div class="pageContainer">
    <div class="pageContainer__left">
      <addProductForm class="pageContainer__form"/>
    </div>
    <div class="pageContainer__right"> 
      <div class="pageContainer__right__sortContainer">
        <sortBlock />
      </div>
      <productCards class="pageContainer__cards"/>
    </div>
    <confirmModal />
  </div>
</template>

<script>
import addProductForm from '../components/addProductForm'
import productCards from '../components/productCards'
import sortBlock from '../components/sortBlock'
import confirmModal from '../components/confirmModal'

export default {
  name: 'IndexPage'
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

    &__left {
      width: 25%;
      position: sticky;
      top: 0;
    }

    &__right {
      width: 75%;

      &__sortContainer {
        display: flex;
        justify-content: flex-end;
        align-items: center;
        margin-bottom: 16px;
      }
    }
  }
</style>
