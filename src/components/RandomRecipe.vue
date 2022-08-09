<template>
  <div>
  <!-- <b-card :title="recipe.title" :img-src="recipe.image" img-alt="Image" img-top tag="article" style="max-width: 20rem;" class="mb-2"> -->
    <b-card no-body v-bind:title="recipe.title" img-top tag="article" style="max-width: 20rem;" class="mb-2">
      <router-link :to="{ name: 'RecipeViewPage', params:{id:recipe.id} } ">
      <b-card-img :src="recipe.image"/> 
      </router-link>
      <b-card-title v-bind:title="recipe.title"></b-card-title>
      <b-card-text>
      <ul class="recipe-overview" style="list-style-type: none;">
          <li><b-icon-heart-fill style="font-size: 2rem;"></b-icon-heart-fill><span> Likes:</span> {{ recipe.popularity}}</li>
          <li><b-icon-clock-history style="font-size: 2rem;"></b-icon-clock-history><span> Time:</span> {{recipe.readyInMinutes}} </li>
          <li><b-icon icon="egg" style="font-size: 2rem;"></b-icon><span>Vegan:</span> {{recipe.vegan}}</li>
          <li><b-icon-egg-fill style="font-size: 2rem;"></b-icon-egg-fill><span>Vegeterian:</span> {{recipe.vegetarian}}</li>
          <li><b-icon-x-circle-fill style="font-size: 2rem;"></b-icon-x-circle-fill><span>Gluten-Free:</span> {{recipe.glutenFree}}</li>

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
export default {
    name: 'RandomRecipe',
    props: {
     recipe: {
      type: Object,
      required: true
    }
    },
    data() {
      return {
        favortied:'',
        watched:'',
      };
    },
    mounted() {
        this.getFavorites();
        this.getWatched();
    },
    methods: {
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
              recipeId: this.recipe.id
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
            if(recipes[i] == this.recipe.id){
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
      //     const parsed = JSON.stringify(this.recipe.id);
      //     this.$root.store.setQuery3(parsed);
      //     const response = await this.axios.post(this.$root.store.server_domain+"/users/user_watched_recipe",
      //       {
      //         recipeId: this.recipe.id
      //       }
      //     );
      //   } catch (error) {
      //     console.log(error);
      //   }
      // }
    },
};
</script>

<style lang="scss" scoped>
.recipe-preview {
  display: inline-block;
  width: 90%;
  height: 100%;
  position: relative;
  margin: 10px 10px;
}
.recipe-preview > .recipe-body {
  width: 100%;
  height: 200px;
  position: relative;
}

.recipe-preview .recipe-body .recipe-image {
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
  display: block;
  width: 98%;
  height: auto;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  background-size: cover;
}

.recipe-preview .recipe-footer {
  width: 100%;
  height: 50%;
   overflow: hidden; 
}

.recipe-preview .recipe-footer .recipe-title {
  padding: 10px 10px;
  width: 100%;
  font-size: 12pt;
  text-align: left;
  white-space: nowrap;
  overflow: hidden; 
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
}

.recipe-preview .recipe-footer ul.recipe-overview {
  padding: 5px 10px;
  width: 100%;
  display: -webkit-box;
  display: -moz-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  box-flex: 1;
  -webkit-flex: 1 auto;
  -ms-flex: 1 auto;
  flex: 1 auto;
  table-layout: fixed;
  margin-bottom: 0px;
    list-style-type: none;
}

.recipe-preview .recipe-footer ul.recipe-overview li {
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  -ms-box-flex: 1;
  box-flex: 1;
  -webkit-flex-grow: 1;
  flex-grow: 1;
  width: 90px;
  display: table-cell;
  text-align: center;
}

</style>