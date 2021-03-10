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
      lessons: [
        /*{
          id: 0,
          title: "Maths",
          location: "London",
          price: 150,
          spaces: 5,
          image: "~/components/images/math.png",
        },
        {
          id: 1,
          title: "English",
          location: "Oxford",
          price: 100,
          spaces: 5,
          image: "~/components/images/english.png",
        },
        {
          id: 2,
          title: "Physics",
          location: "Manchester",
          price: 200,
          spaces: 5,
          image: "~/components/images/physics.png",
        },
        {
          id: 3,
          title: "Chemistry",
          location: "Bristol",
          price: 120,
          spaces: 5,
          image: "~/components/images/chem.png",
        },
        {
          id: 4,
          title: "Music",
          location: "Brighton",
          price: 200,
          spaces: 5,
          image: "~/components/images/music.png",
        },
        {
          id: 5,
          title: "Theatre",
          location: "Edinburgh",
          price: 180,
          spaces: 5,
          image: "~/components/images/theatre.png",
        },*/
      ],
    };
  },
  created: function(){
    fetch('https://tester3145.herokuapp.com/collection/lessons').then(
        function(response){
            response.json().then(
                function(json){
                    app.lessons = json
                }
            )
        }
    )
},
  methods: {
      addProduct(event){
          if(event.item.spaces > 0){
              event.item.spaces -= 1
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