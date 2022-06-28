<template>
    <div >
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
            Instructions: ''
        };
    },
    mounted() {
    },
    methods: {
      getInstructions(){
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