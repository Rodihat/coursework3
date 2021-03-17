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
    <button @tap="bought">Buy now</button>
  </StackLayout>
</template>

<script>
export default {
  name: "Cart",
  props: ["cart"],
  data() {
    return {
      name: "",
      number: "",
    };
  },
  methods: {
    removeItem(event) {
      this.$emit("removeItem", event.item);
      event.item.spaces++
    },
    bought(){
      this.$emit("hasBought")
    }
  },
};
</script>

<style>
</style>
