<template>
    <StackLayout>
        <Label class="h2 p-10" textWrap="true" text="Select a product to add to cart"></Label>
        <ListView for='lesson in lessons' @itemTap='addProduct'>
            <v-template>
                <StackLayout>
                        <Image v-bind:src="lesson.image" loadMode="async"/>
                        <Label :text='lesson.topic'></Label>
                        <Label :text="`Location: ${lesson.location}`"></Label>
                        <Label :text="`Price: ${lesson.price}`"></Label>
                        <Label :text="`Spaces: ${lesson.spaces}`"></Label>
                </StackLayout>
            </v-template>
        </ListView>    
    </StackLayout>
</template>

<script>
export default {
  name: "Lessons",
  data() {
    return {
      lessons: [],
    };
  },
created() {
    fetch("https://tester3145.herokuapp.com/collection/lessons")
      .then((res) => res.json())
      .then((data) => {
        this.lessons = data;
      });
  },
  methods: {
      addProduct(event){
          if(event.item.spaces > 0){
              this.$emit('addProduct', event.item)
          }else{
              alert("No more spaces left !")
          }
      },
  },
};
</script>

<style>
    .box{
        border: solid blue;
    }
</style>
