<template>
  <page style='background-color: azure;'>
      <ActionBar title="Tutor lessons"/>
      <Label text='Book an afterschool lesson below' class="h2 text-center"></Label>
  
      <TabView androidTabsPosition="botton">

        <TabViewItem title="Lessons" class="h2 text-capitalize">
          <Lessons @addProduct="addToCart"/>
        </TabViewItem>

        <TabViewItem title="Checkout" class="h2 text-capitalize">
          <Checkout :cart="cart" @removeItem="removeFromCart" @hasBought="submitOrder" />
        </TabViewItem>
      </TabView>
  </page>
</template>

<script>
import Lessons from "./Lessons.vue";
import Checkout from "./Checkout.vue";
export default {
  name: "App",
  components: {Lessons, Checkout},
  data() {
    return {
      sitename: "After School Club",
      cart: [],
      orders: []
    };
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
      //alert("Added to cart: " + product.title)
    },
    removeFromCart(item) {
      const index = this.cart.indexOf(item);
      this.cart.splice(index, 1);
    },
    submitOrder(){
      if (this.cart.length > 0 ){
        alert("Order Submitted !")
        this.cart = []
        //Add to order via mongo here       
      } else {
        alert("Nothing in cart to order.")
      }
    },
  }
};
</script>

<style>

</style>
