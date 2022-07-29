<template>
  <div  class="productZone">
    <div v-for="product in arrayOfProducts" v-bind:key="product">
      <ProductCard :product="product"/>
    </div>
  </div>
</template>

<script>
import ProductCard from "@/components/ProductCard";
export default {
  components: {ProductCard},
  data() {
    return {

    }
  },
  props: {
    arrayOfProducts: {
      type: Array,
      required: true,
    }
  },
}
</script>

<style scoped>
 .productZone {
   display: flex;
   margin-top: 83px;
   flex-wrap: wrap;
   gap: 16px;
   margin-left: 16px;
 }
</style>