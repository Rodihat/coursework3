<template>
  <StackLayout>
    <Label class="h2 p-10" textWrap="true" text="Select a product to remove it"/>
    <ListView for="item in cart" @itemTap="removeItem">
      <v-template>
        <StackLayout>
          <Label :text="item.topic"></Label>
          <Label :text="`Price: ${item.price}`"></Label>
          <Label :text="`Spaces left: ${item.spaces}`"></Label>
        </StackLayout>
      </v-template>
    </ListView>
    <TextField hint="Name" v-model="name" />
    <TextField hint="Number" v-model="number" />
    <button @tap="submitOrder">Buy now</button>
  </StackLayout>
</template>

<script>
export default {
  name: "Cart",
  props: ["cart"],
  data() {
    return {
      name: "",
      number: ""
    };
  },
  methods: {
    removeItem(event) {
      this.$emit("removeItem", event.item);
      event.item.spaces++
    },
    submitOrder(){
      var lessonTitle = []
      if (this.cart.length > 0 && this.name !== "" && this.number !== ""){
        var i = 0
        while (i < this.cart.length){
          lessonTitle.push(this.cart[i].topic)
          i++
        }
        const newProduct = {name:this.name, number:this.number,LessonsOrdered:lessonTitle}
            fetch('https://tester3145.herokuapp.com/collection/orders', {
              method: 'POST', 
              headers: {
              'Content-Type': 'application/json',
              },
              body: JSON.stringify(newProduct),
              })
              .then(response => response.json())
              .then(responseJSON => {
              console.log('Success:', responseJSON);
              alert("Order added!")
              })
      this.cart = []
      } else {
        alert("Ensure cart has item and full details are entered.")
      }
    }
  },
};
</script>

<style>
</style>
