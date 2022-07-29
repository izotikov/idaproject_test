<template>
  <div class="productFolder">
    <img class="productFolder__productImage" v-bind:src="require('../img/ProductPhoto.png')" alt="product_photo">
    <span class="productFolder__NameOfTheProduct">{{product.name}}</span>
    <div class="productFolder__DescriptionOfTheProduct">{{product.description}}
    </div>
    <span class="productFolder__price">{{product.price}} руб.</span>
  </div>
</template>

<script>
export default {
  data() {
    return {

    }
  },
  props: {
    product: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
  .productFolder {
    display: flex;
    width: 332px;
    height: 423px;
    flex-direction: column;
    font-family: 'Source Sans Pro', sans-serif;
    color: #3F3F3F;
    background-color: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    transition: transform .2s;
  }
  .productFolder:hover {
    cursor: pointer;
    background-color: #eee;
    transform: scale(1.05);
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.7);
  }
  .productFolder__productImage {
    width: 100%;
  }

  .productFolder__NameOfTheProduct {
    font-weight: 600;
    font-size: 20px;
    padding: 16px;
  }
  .productFolder__DescriptionOfTheProduct {
    font-weight: 400;
    width: 90%;
    align-self: center;
    font-size: 16px;
  }
  .productFolder__price {
    font-size: 24px;
    font-weight: 600;
    padding: 24px;
    margin-top: 8px;
  }
</style>