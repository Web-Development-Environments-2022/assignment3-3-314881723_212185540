<template>
  <div>
    <b-card no-body v-bind:title="Recipe.title" img-top tag="article" style="max-width: 20rem;" class="mb-2">
      <router-link :to="{ name: 'RecipeViewPage' }" @click.native="Watch()">
      <b-card-img :src="Recipe.image"/> 
      </router-link>
      <b-card-title v-bind:title="Recipe.title"></b-card-title>
      <b-card-text>
        <ul class="recipe-overview" style="list-style-type: none;">
          <li><b-icon-heart-fill style="font-size: 2rem;"></b-icon-heart-fill><span> Likes:</span> {{ Recipe.popularity}}</li>
          <li> <b-icon-clock-history style="font-size: 2rem;"></b-icon-clock-history><span> Time:</span> {{Recipe.readyInMinutes}} </li>
          <li><b-icon icon="egg" style="font-size: 2rem;"></b-icon><span>Vegan:</span> {{Recipe.vegan}}</li>
          <li><b-icon-egg-fill style="font-size: 2rem;"></b-icon-egg-fill><span>Vegeterian:</span> {{Recipe.vegetarian}}</li>
          <li><b-icon-x-circle-fill style="font-size: 2rem;"></b-icon-x-circle-fill><span>Gluten-Free:</span> {{Recipe.glutenFree}}</li>
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
  name: 'PreviewRecipe',
  props: {
    recipe_id: {
      type: Number,
      required: true
    },
  },
  data() {
    return {
      Recipe:'',
      favortied:'',
      watched:''
    };
  },
  mounted() {
    this.getRecipe_Object();
    this.getFavorites();
    this.getWatched();
    
  },
  methods: {  
    async getRecipe_Object(){
      let recipe_id_String=JSON.stringify(this.recipe_id);
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain+"/recipes/"+recipe_id_String
        );
        const RecipeData = response.data;
        this.Recipe=RecipeData;
      } catch (error) {
        console.log(error);
      }
    },
    async getFavorites(){
        try {
          const response = await this.axios.get(this.$root.store.server_domain+"/users/favorites",);
          const RecipesData = response.data;
          let recipes=RecipesData;
          for(let i = 0; i<recipes.length;i++){
            if(recipes[i].id == this.recipe_id){
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
            recipeId: this.recipe_id
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
        // console.log("current recipe")
        // console.log(this.recipe_id)
        // console.log("all recipes in watched")
        // console.log(recipes)
        for(let i = 0; i<recipes.length;i++){
          if(recipes[i] == this.recipe_id){
            this.watched = true;
            return;
          }
        }
        this.watched = '';
      } catch (error) {
        console.log(error);
      }
    },
    async Watch(){
      try {
        const response = await this.axios.post(this.$root.store.server_domain+"/users/user_watched_recipe",
          {
            recipeId: this.recipe_id
          }
        );
        const parsed = JSON.stringify(this.recipe_id);
        this.$root.store.setQuery3(parsed);
      } catch (error) {
        console.log(error);
      }
    }
  },
};
</script>

<style lang="scss" scoped>
b-card.title{
  color: blue;
}
div{

width: 310px;
box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
  /* in order: x offset, y offset, blur size, spread size, color */
  /* blur size and spread size are optional (they default to 0) */

}

</style>