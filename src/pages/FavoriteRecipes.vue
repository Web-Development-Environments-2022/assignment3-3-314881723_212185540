<template>
    <div class="container2" style="margin-left:140px; width: 1500px;">
        <h1 class="title" style="margin-left:160px" >My Favorite Recipes:</h1>
        <section style="margin-left: 180px" class="ReturnedRecipes" v-if="this.recipes != ''">
            <b-card-group deck>
                <PreviewRecipeOnly v-for="recipe in this.recipes"
                :key="recipe.id"
                :Recipe="recipe"
                ></PreviewRecipeOnly>         
            </b-card-group>
        </section>
    </div>
</template>

<script>
import PreviewRecipeOnly from "../components/PreviewRecipeOnly";
export default {
    name:"FavoriteRecipes",
    components:{
        PreviewRecipeOnly
    },
    data(){
        return{
            recipes: '',
        }
        
    },
    mounted(){
        this.getFavoriteRecipes();
    },
    methods:{
      async getFavoriteRecipes(){
        try {
          const response = await this.axios.get("http://localhost:80"+"/users/favorites",);
          const RecipesData = response.data;
          this.recipes=RecipesData;
          console.log(this.recipes)
        } catch (error) {
          console.log(error);
        }
      }
    },
    
}
</script>

<style>

</style>