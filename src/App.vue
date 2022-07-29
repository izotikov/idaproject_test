<template>
  <div class="mainPage">
    <div>
      <div class="mainPage__inscription">
        Добавление товара
      </div>
      <AddProductForm @create="createCard"/>
    </div>
    <RenderProductCard :array-of-products="arrayOfProducts"/>
    <select class="mainPage__sort">
      <option selected>По умолчанию</option>
      <option>По цене (min)</option>
      <option>По цене (max)</option>
      <option>По наименованию</option>
    </select>
  </div>
</template>

<script>
import AddProductForm from "@/components/AddProductForm";
import RenderProductCard from "@/components/RenderProductCard";
import {arrayOfProducts} from "@/arrayOfProducts/arrayOfProducts";
export default {
  components: {RenderProductCard, AddProductForm},
  data() {
    return {
      arrayOfProducts,
    }
  },
  methods: {
    createCard(product) {
      this.arrayOfProducts.push(product);
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@200;300;400;600&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.mainPage {
  display: flex;
  background-color: #faf9f7;
  flex-direction: row;
}

.mainPage__inscription {
  font-weight: 600;
  font-size: 28px;
  font-family: 'Source Sans Pro', sans-serif;
  color: #3F3F3F;
  padding: 32px 32px 16px 32px;
}
.mainPage__sort {
  border: none;
  outline: none;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  padding: 10px 16px;
  font-size: 12px;
  color: #B4B4B4;
  position: absolute;
  right: 31px;
  top: 31px;
}
.mainPage__sort::placeholder {
  color: #B4B4B4;
}

</style>