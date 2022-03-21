<template>
  <div>
    <p>Items in cart : {{ cartList.length }}</p>
  </div>
  <div class="flex w-full justify-items-center grid grid-cols-4 gap-14 text-center mt-14">
    <ItemComponent @cartListToHomePage="onItemClick"></ItemComponent>
  </div>
</template>

<script>

import ItemComponent from '@/components/ItemComponent.vue'

export default {
  name: "HomePage",
  components: {
    ItemComponent
  },
  data() {
    return {
      items: [],
      cartList: []
    }
  },
  methods: {
    onItemClick(value){
      console.log(value)
      this.cartList = value
    }
  }
}


</script>

<style scoped>

</style>