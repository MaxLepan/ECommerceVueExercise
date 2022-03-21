<template>
  <div v-for="item in items"
       :key="item.itemName"
       @click="itemInCartCheck(item)"
       :class="[cartList.includes(item) ? 'border-indigo-500' : 'border-indigo-100']"
       class="w-72 h-min bg-indigo-100 border-2">
    <img :src="item.itemImage" class="w-full">
    <div class="mt-2 mb-2">
      <p>{{ item.itemName }}</p>
      <p>${{ item.itemPrice }}</p>
    </div>
    <div v-if="cartList.includes(item)">
      <button class="border-indigo-400">
        Add to cart
      </button>
    </div>
  </div>
</template>

<script>
import {default as axios} from "axios";

export default {
  name: "ItemComponent",
  data() {
    return {
      items: [],
      cartList: []
    }
  },
  methods: {
    async getProducts() {
      try {
        const response = await axios.get('https://fakestoreapi.com/products')
        const data = response.data
        console.log(data)

        data.forEach(datum => {
          let item = {itemName: datum.title, itemPrice: datum.price, itemImage: datum.image}
          this.items.push(item)
        })

        //console.log(this.items)

      } catch (e) {
        console.log(e)
      }
    },
    itemInCartCheck(item) {

      if(this.cartList.includes(item)){
        this.cartList.splice(this.cartList.indexOf(item), 1)
      } else {
        this.cartList.push(item)
      }

      this.$emit('cartListToHomePage', this.cartList)

    }
  },
  created() {
    this.getProducts()
  }
}
</script>

<style scoped>

</style>