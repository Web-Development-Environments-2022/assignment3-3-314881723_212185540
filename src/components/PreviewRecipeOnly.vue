<template>
    <!-- <div>
        <b-card
        :title="Recipe.title"
        :img-src="Recipe.image"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 20rem; padding-right: 10px; "
        class="mb-1">
            <div class=""></div>
            <b-card-text >
            <ul class="recipe-overview" style="list-style-type: none; padding-left: 10px;">
                <li><b-icon-heart-fill style="font-size: 2rem;"></b-icon-heart-fill><span> Likes:</span> {{ Recipe.popularity}}</li>
                <li> <b-icon-clock-history style="font-size: 2rem;"></b-icon-clock-history><span> Time:</span> {{Recipe.readyInMinutes}} </li>
                <li><b-icon icon="egg" style="font-size: 2rem;"></b-icon><span>Vegan:</span> {{Recipe.vegan}}</li>
                <li><span>Vegeterian:</span> {{Recipe.vegetarian}}</li>
                <li><span>Gluten-Free:</span> {{Recipe.glutenFree}}</li>
                <li :href="getInstructions()"><span>Instructions: <br></span> {{Instructions}}</li>
            </ul> 
            </b-card-text>
        </b-card>
    </div> -->
    <div>
    <!-- <b-card :title="recipe.title" :img-src="recipe.image" img-alt="Image" img-top tag="article" style="max-width: 20rem;" class="mb-2"> -->
      <b-card no-body v-bind:title="Recipe.title" img-top tag="article" style="max-width: 20rem;" class="mb-2">
        <router-link :to="{ name: 'RecipeViewPage', params:{id:Recipe.id} } ">
        <b-card-img :src="Recipe.image"/> 
        </router-link>
        <b-card-title v-bind:title="Recipe.title"></b-card-title>
        <b-card-text>
        <ul class="recipe-overview" style="list-style-type: none;">
            <li><b-icon-heart-fill style="font-size: 2rem;"></b-icon-heart-fill><span> Likes:</span> {{ Recipe.popularity}}</li>
            <li><b-icon-clock-history style="font-size: 2rem;"></b-icon-clock-history><span> Time:</span> {{Recipe.readyInMinutes}} </li>
            <li><b-icon icon="egg" style="font-size: 2rem;"></b-icon><span>Vegan:</span> {{Recipe.vegan}}</li>
            <li><b-icon-egg-fill style="font-size: 2rem;"></b-icon-egg-fill><span>Vegeterian:</span> {{Recipe.vegetarian}}</li>
            <li><b-icon-x-circle-fill style="font-size: 2rem;"></b-icon-x-circle-fill><span>Gluten-Free:</span> {{Recipe.glutenFree}}</li>
            <li :href="getInstructions()"><span>Instructions: <br></span> {{Instructions}}</li>

            <li>
              <span>Favorite:</span>
              <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" style="margin-left:10px" v-if="this.favortied == true" checked disabled>
              <input class="form-check-input" type="checkbox" value="" @click="Favorite()" id="flexCheckDefault" style="margin-left:10px" v-else-if="this.favortied != true">
            </li>
            <li>
              <span>Watched:</span>
              <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" style="margin-left:10px" v-if="this.watched == true" checked disabled>
              <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" style="margin-left:10px" v-else-if="this.watched != true" disabled>
            </li>
        </ul> 
      </b-card-text>
      </b-card>
    </div>
</template>

<script>
import { faLeftRight } from '@fortawesome/free-solid-svg-icons';

export default {
    name: 'PreviewRecipeOnly',
    props: {
      recipe_id: {
        type: Number,
        required: false
      },
      Recipe: {
        type: Object,
        required: false,
        default() {
        return undefined;
      }
      },
    },
    data() {
      return {
        Instructions: '',
        favortied:'',
        watched:'',
      };
    },
    mounted() {
      this.getFavorites();
      this.getWatched();
    },
    methods: {
      // async getFavorites(){
      //   try {
      //     const response = await this.axios.get(this.$root.store.server_domain+"/users/favorites",);
      //     console.log(response)
      //     const RecipesData = response.data;
      //     let recipes_new=RecipesData;
      //     console.log("current recipe")
      //     console.log(this.Recipe.id)
      //     console.log("all recipes in favorites")
      //     console.log(recipes_new)
      //     for(let i = 0; i<recipes_new.length;i++){
      //       console.log("in recipes iterator")
      //       console.log(recipes_new[i])
      //       if(recipes_new[i].id == this.Recipe.id){
      //         this.favortied = true;
      //         return;
      //       }
      //     }
      //     this.favortied = '';
      //   } catch (error) {
      //     console.log(error);
      //   } 
      // },
      async getFavorites(){
        try {
          const response = await this.axios.get(this.$root.store.server_domain+"/users/favoritesIDOnly",);
          const recipesIDS = response.data;
          //let recipes=RecipesData;
          for(let i = 0; i<recipesIDS.length;i++){
            if(recipesIDS[i] == this.recipe.id){
              this.favortied = true;
              return;
            }
          }
          this.favortied = '';
        } catch (error) {
          console.log(error);
        }
        
      },
      async Favorite(){
        try {
          const response = await this.axios.post(this.$root.store.server_domain+"/users/favorites",
            {
              recipeId: this.Recipe.id
            }
          );
          this.favortied = true;
        } catch (error) {
          console.log(error);
        }
      },
      async getWatched(){
        try {
          const response = await this.axios.get(this.$root.store.server_domain+"/users/user_indication_recipe_NEW",);
          const RecipesData = response.data;
          let recipes=RecipesData;
          for(let i = 0; i<recipes.length;i++){
            if(recipes[i] == this.Recipe.id){
              this.watched = true;
              return;
            }
          }
          this.watched = '';
        } catch (error) {
          console.log(error);
        }
      },
      // async Watch(){
      //   try {
      //     const parsed = JSON.stringify(this.Recipe.id);
      //     this.$root.store.setQuery3(parsed);
      //     const response = await this.axios.post(this.$root.store.server_domain+"/users/user_watched_recipe",
      //       {
      //         recipeId: this.Recipe.id
      //       }
      //     );
      //   } catch (error) {
      //     console.log(error);
      //   }
      // },
      getInstructions(){
        //console.log(this.Recipe)
        if(this.Recipe.analyzedInstructions == undefined && this.Recipe.instructions != undefined){
          this.Instructions = this.Recipe.instructions;
        }
        else{
          let returnedstring =''
          for (let i = 0; i < this.Recipe.analyzedInstructions.length ; i++){ //go over every Instruction
            returnedstring += 'Part ' + (i+1) + ': ';
            for (let j = 0; j < this.Recipe.analyzedInstructions[i].steps.length ; j++){ //go over every step
              returnedstring += 'Step ' + (j+1) + ': ' + this.Recipe.analyzedInstructions[i].steps[j].step + ' ';
            }
          } 
          this.Instructions = returnedstring;
        }
      },
    },
};
</script>

<style lang="scss" scoped>
b-card.title{
  color: blue;
}
div{
    margin-top:10px;
    margin-right:10px;
    margin-bottom: 10px;
    width: 310px;
    box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
  /* in order: x offset, y offset, blur size, spread size, color */
  /* blur size and spread size are optional (they default to 0) */

}

</style>