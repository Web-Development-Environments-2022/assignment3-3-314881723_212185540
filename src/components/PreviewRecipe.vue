<template>
    <div>
         <b-card
    :title="Recipe.title"
    :img-src="Recipe.image"
    img-alt="Image"
    img-top
    tag="article"
    style="max-width: 20rem;"
    class="mb-2">
  <div class=""></div>
    <b-card-text>
    <ul class="recipe-overview" style="list-style-type: none;">
        <li><b-icon-heart-fill style="font-size: 2rem;"></b-icon-heart-fill><span> Likes:</span> {{ Recipe.popularity}}</li>
        <li> <b-icon-clock-history style="font-size: 2rem;"></b-icon-clock-history><span> Time:</span> {{Recipe.readyInMinutes}} </li>
        <li><b-icon icon="egg" style="font-size: 2rem;"></b-icon><span>Vegan:</span><font-awesome-icon icon="fa-solid fa-leaf" /> {{Recipe.vegan}}</li>
        <li><span>Vegeterian:</span><font-awesome-icon icon="fa-solid fa-salad" /> {{Recipe.vegetarian}}</li>
        <li><span>Gloten:</span><font-awesome-icon icon="fa-solid fa-salad" /> {{Recipe.vegetarian}}</li>
        <li><font-awesome-icon icon="fa-solid fa-user-secret" /> <span>already Watch:</span>{{IndicationAboutRecipe.alreadyWatchFlag}}</li>
        <li><b-icon icon="cloud-download" style="font-size: 2rem;"></b-icon> <span>already Save:</span>{{IndicationAboutRecipe.alreadySaveFlag}}</li>
        
      </ul> 
   </b-card-text>
  </b-card>

        <!-- <h1>title:{{Recipe.title}}</h1>
        <h1>image:{{Recipe.image}}</h1>
        <h1>likes:{{Recipe.popularity}}</h1>
        <h1>time:{{Recipe.readyInMinutes}}</h1>
        <h1>vegan:{{Recipe.vegan}}</h1>
        <h1>vegetarian:{{Recipe.vegetarian}}</h1>
        <h1>glutenFree:{{Recipe.glutenFree}}</h1>
        <h1>alreadyWatchFlag:{{IndicationAboutRecipe.alreadyWatchFlag}}</h1>
        <h1>alreadySaveFlag:{{IndicationAboutRecipe.alreadySaveFlag}}</h1> -->
        
    </div>
</template>

<script>
import { faLeftRight } from '@fortawesome/free-solid-svg-icons';

export default {
    name: 'PreviewRecipe',
    props: {
     recipe_id: {
      type: Object,
      required: true
    },
    IndicationAboutRecipe: {
      type: Object,
      required: false,
      default() {
      return undefined;
    }
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
            
        };
    },

    mounted() {
      
        this.get_Indication_Recipe_Object();
        this.getRecipe_Object();
    },

    methods: {
      
    async getRecipe_Object(){
      
      let recipe_id_String=JSON.stringify(this.recipe_id);
      
       try {
        const response = await this.axios.get(
           "http://localhost:80"+"/recipes/"+recipe_id_String
        );
        const RecipeData = response.data;
        this.Recipe=RecipeData;
      } catch (error) {
        console.log(error);
      }

  },

      async get_Indication_Recipe_Object(){
       try {
        const response = await this.axios.get(
           "http://localhost:80"+"/users/user_indication_recipe",
             {
            recipeId: this.recipe_id
          }
        );
        const RecipeData = response.data;
        this.IndicationAboutRecipe=RecipeData;
      } catch (error) {
        console.log(error);
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

width: 310px;
box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
  /* in order: x offset, y offset, blur size, spread size, color */
  /* blur size and spread size are optional (they default to 0) */

}

</style>