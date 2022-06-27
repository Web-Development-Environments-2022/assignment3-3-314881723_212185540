<template>
   <div class="container2" style="margin-left:140px; width: 1500px;">
    <h1 class="title" style="margin-left:160px" >Search Recipes</h1>
    <!-- SearchBar -->
    <section class="search-bar">
      <div class="container1" style="margin-left:300px">
        <div class="row">
          <form>
            <div>
              <div class="input-group">
                <input type="search"  v-model="query" placeholder="Search for recipes" class="form-control" >
                <div class="mx-auto">
                  <b-dropdown id="dropdown-1" :text="num">
                    <b-dropdown-item @click="changeTextNum('5')">5</b-dropdown-item>
                    <b-dropdown-item @click="changeTextNum('10')">10</b-dropdown-item>
                    <b-dropdown-item @click="changeTextNum('15')">15</b-dropdown-item>
                  </b-dropdown>
                  <b-dropdown id="dropdown-2" :text="cuisine">
                    <b-dropdown-item @click="changeTextCuisine('Cuisine')">No Cuisine Filter</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('African')">African</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('American')">American</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('British')">British</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Cajun')">Cajun</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Caribbean')">Caribbean</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Chinese')">Chinese</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Eastern European')">Eastern European</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('European')">European</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('German')">German</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Greek')">Greek</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Indian')">Indian</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Irish')">Irish</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Italian')">Italian</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Japanese')">Japanese</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Jewish')">Jewish</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Korean')">Korean</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Latin American')">Latin American</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Mediterranean')">Mediterranean</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Mexican')">Mexican</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Middle Eastern')">Middle Eastern</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Nordic')">Nordic</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Southern')">Southern</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Spanish')">Spanish</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Thai')">Thai</b-dropdown-item>
                    <b-dropdown-item @click="changeTextCuisine('Vietnamese')">Vietnamese</b-dropdown-item>
                  </b-dropdown>
                  <b-dropdown id="dropdown-3" :text="diet">
                    <b-dropdown-item @click="changeTextDiet('Diet')">No Diet Filter</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Gluten Free')">Gluten Free</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Ketogenic')">Ketogenic</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Vegetarian')">Vegetarian</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Lacto-Vegetarian')">Lacto-Vegetarian</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Ovo-Vegetarian')">Ovo-Vegetarian</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Vegan')">Vegan</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Pescetarian')">Pescetarian</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Paleo')">Paleo</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Primal')">Primal</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Low FODMAP')">Low FODMAP</b-dropdown-item>
                    <b-dropdown-item @click="changeTextDiet('Whole30')">Whole30</b-dropdown-item>
                  </b-dropdown>
                  <b-dropdown id="dropdown-4" :text="intolerance">
                    <b-dropdown-item @click="changeTextIntolerance('Intolerance')">No Intolerance Filter</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Dairy')">Dairy</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Egg')">Egg</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Gluten')">Gluten</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Grain')">Grain</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Peanut')">Peanut</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Seafood')">Seafood</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Sesame')">Sesame</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Shellfish')">Shellfish</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Soy')">Soy</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Sulfite')">Sulfite</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Tree Nut')">Tree Nut</b-dropdown-item>
                    <b-dropdown-item @click="changeTextIntolerance('Wheat')">Wheat</b-dropdown-item>
                  </b-dropdown>
                </div>
                <div class="input-group-append">
                  <button type="sumbit" @click="searchRecipe()" class="btn btn-link"><b-icon-search></b-icon-search></button>
                </div>
              </div>
            </div>
          </form>
        </div>
      </div>
    </section>
    <!-- ReturnedRecipes: -->
    <div>
      <div></div>
    </div>
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
  name:"SearchPage",
  components:{
    PreviewRecipeOnly
  },
  data(){
    return{
      cuisine:'Cuisine',
      diet:'Diet',
      intolerance:'Intolerance',
      num:'5',

      query:'',
      recipes:'',
    }
  },
  methods:{
    changeTextCuisine(x){
      this.cuisine=x;
    },
    changeTextDiet(x){
      this.diet=x;
    },
    changeTextIntolerance(x){
      this.intolerance=x;
    },
    changeTextNum(x){
      this.num=x
    },
    async searchRecipe(){
      // let query=JSON.stringify(this.query);
      // let num = JSON.stringify(this.num);
      let cuisineFixed = '';
      let dietFixed = '';
      let intoleranceFixed ='';
      if(this.cuisine != 'Cuisine'){
        cuisineFixed = this.cuisine
      }
      if(this.diet != 'Diet'){
        dietFixed = this.diet;
      }
      if(this.intolerance != 'Intolerance'){
        intoleranceFixed = this.intolerance;
      }
      try {
        const response = await this.axios.get(
           "http://localhost:80"+"/recipes/search/query/"+this.query+"/amount/"+this.num,
           {
              params:{
                cuisine:cuisineFixed,
                diet:dietFixed,
                intolerances:intoleranceFixed
              } 
           }
        );
        const RecipesData = response.data;
        this.recipes=RecipesData;
        console.log(this.recipes)
      } catch (error) {
        console.log(error);
      }
    },
  },
}
</script>

<style>
.dropdown-menu {
    max-height: 280px;
    overflow-y: auto;
}
</style>
