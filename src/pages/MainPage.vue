<template>
  <div class="container">     
    <b-container fluid class="p-5 bg-dark" style=" width: 380px; margin-left: -60px;" >
      <h3 style="margin-left:0px; margin-top: -30px;"><b-badge>Show random Recipes</b-badge></h3>
      <RandomRecipe :recipe="RecipeRandom1" ></RandomRecipe>
      <RandomRecipe :recipe="RecipeRandom2" ></RandomRecipe>
      <RandomRecipe :recipe="RecipeRandom3" ></RandomRecipe>
      <b-button variant="info" @click="reloadPage"><b-spinner type="grow" label="Loading..."></b-spinner>  <span style=" margin-bottom: 500px;">Shuffle</span></b-button>
    </b-container>
    <div id="Guest" v-if="!$root.store.username" >
      <div>


      </div>  
      <LoginPage  class="comp" style="margin-top:-1250px ; margin-right: 20px;" ></LoginPage>
    </div>
    <div id="UserLoggedIn" style="margin-top:-1500px ; margin-left: 700px;" v-else>
      <h3 style="margin-left:0px; margin-top: -30px; "><b-badge>Show last 3 Watched Recipes</b-badge></h3>
      <PreviewRecipe :recipe_id= "this.LastWatch1"  v-if="this.LastWatch1" ></PreviewRecipe>
      <PreviewRecipe :recipe_id= "this.LastWatch2"  v-if="this.LastWatch2" ></PreviewRecipe>
      <PreviewRecipe :recipe_id= "this.LastWatch3"  v-if="this.LastWatch3" ></PreviewRecipe>
    </div>
  </div>
</template>

<script>
import { BIconLayoutTextWindowReverse } from "bootstrap-vue";
import RandomRecipe from "../components/RandomRecipe";
import LoginPage from "../pages/LoginPage";
import PreviewRecipe from "../components/PreviewRecipe";
export default {
  components: {
    RandomRecipe,
    LoginPage,
    PreviewRecipe,
  },
  props: {
    // LastWatch1: Object,
    // LastWatch2: Object,
    // LastWatch3: Object
  },
  computed: {
    values() {
      return this.LastWatch1;
    }
  },
  data(){
    return{
      RecipeRandom1:{},
      RecipeRandom2:{},
      RecipeRandom3:{},
      LastWatch1:'',
      LastWatch2:'',
      LastWatch3:''
    }
  },
  methods: {
    reloadPage() {
      window.location.reload();
    },

    async getRandom3Recipes(){
      try {
        const response = await this.axios.get(
           this.$root.store.server_domain+"/recipes/random",
        );
        const RecipeData = response.data;
        this.RecipeRandom1=RecipeData[0];
        this.RecipeRandom2=RecipeData[1];
        this.RecipeRandom3=RecipeData[2];
      }catch (error) {
        console.log(error);
      }
    },

    async getUserLast3Watch(){
      try {
        const response = await this.axios.get(
           this.$root.store.server_domain+"/users/user_last_3_watch",
        );
        await setTimeout(10000);
        const RecipeData = response.data;
        this.LastWatch1=RecipeData[0].History_Watch_R1;
        this.LastWatch2=RecipeData[0].History_Watch_R2;
        this.LastWatch3=RecipeData[0].History_Watch_R3;
      }catch (error) {
        console.log(error);
      }
    },
  },
  mounted(){
    this.getRandom3Recipes();
    this.getUserLast3Watch();
  }
};
</script>

<style lang="scss" scoped>
.RandomRecipes {
  margin: 10px 0 10px;
}
.blur {
  -webkit-filter: blur(5px); /* Safari 6.0 - 9.0 */
  filter: blur(2px);
}
::v-deep .blur .recipe-preview {
  pointer-events: none;
  cursor: default;
}
.elemnt_row{
padding: 20px;
}
</style>
