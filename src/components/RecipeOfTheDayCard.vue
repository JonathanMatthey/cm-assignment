<template>
  <div class="recipe-card" :style="recipeImageStyle" @click="$emit('click')">
    <div class="recipe-details">
      <div class="recipe-title-prefix">Recipe of the day</div>
      <h3 class="recipe-title">{{title}}</h3>
      <StarRating 
        v-bind:rating="rating"
      />
      <div class="recipe-meta">
        <RecipeDuration 
          v-bind:minutes="recipeDurationMinutes"
          v-bind:show-icon="false"
        />
        <EnergyUnit 
          v-bind:value="energyValue"
          v-bind:unit="energyUnit"
          v-bind:show-icon="false"
        />
      </div>
      <div class="recipe-details__bottom-row">
        <MacroDots 
          v-bind:carbs="carbs"
          v-bind:protein="protein"
          v-bind:fats="fats"
          class="macro-dots"
        />
        <div class="btn-learn-more">Learn More</div>
      </div>
    </div>
  </div>
</template>

<script>
  import MacroDots from "./subcomponents/MacroDots.vue";
  import StarRating from "./subcomponents/StarRating.vue";
  import EnergyUnit from "./subcomponents/EnergyUnit.vue";
  import RecipeDuration from "./subcomponents/RecipeDuration.vue";

  export default {
    name: "RecipeOfTheDayCard",
    components: {
      MacroDots,
      StarRating,
      EnergyUnit,
      RecipeDuration,
    },
    props: {
      title: {
        type: String,
        default: 'box'
      },
      rating: {
        type: Number,
        default: 0
      },
      favorite: {
        type: Boolean,
        default: false
      },
      recipeImageUrl: {
        type: String,
        default: ''
      },
      carbs: Number,
      protein: Number,
      fats: Number,
      recipeDurationMinutes: Number,
      energyValue: Number,
      energyUnit: String
    },
    computed: {
      recipeImageStyle() {
        return {
          "background-image": `url(${this.recipeImageUrl})`
        };
      }
    },
  };
</script>

<style scoped>
  .recipe-card{
    max-width:343px;
    background:#eee;
    margin-top:50px;
    text-align:left;
    border-radius:12px;
    background-position: center center;
    background-size: cover;
    position: relative;
    overflow:hidden;
    cursor:pointer;
  }

  .recipe-card:hover .recipe-details{
    background:rgba(0,0,0,0.3)
  }
  
  .recipe-card:hover .btn-learn-more{
    background:rgba(255,255,255,0.5);
  }

  .recipe-title{
    color:#fff;
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 26px;
    display: flex;
    align-items: center;
    margin:0;
    padding:0;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }

  .recipe-details{
    background: rgba(0,0,0,0.45);
    box-sizing:border-box;
    min-height: 220px;
    padding: 36px 24px 24px;
    color:#fff;
    display: flex;
    flex-direction: column;
    flex-flow: column nowrap;
    flex-grow: 1;
    align-items: flex-start;
    transition: background 80ms linear;
    box-sizing:border-box;
  }

  .recipe-title-prefix{
    text-transform:uppercase;
    font-style: normal;
    font-weight: bold;
    font-size: 14px;
    line-height: 16px;
    color: #1BC98E;
  }

  .btn-learn-more{
    background:rgba(255,255,255,0.4);
    border-radius: 15px;
    font-size: 14px;
    line-height: 16px;
    color: #FFFFFF;
    padding: 6px 16px;
    font-weight:bold;
  }

  .recipe-details__bottom-row{
    width:100%;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-top: auto;
  }

  .macro-dots{
    font-size:14px;
  }

  .recipe-meta{
    font-size: 14px;
  }
  .recipe-meta > div{
    display: inline-block;
    margin-right: 10px;
  }
  .recipe-meta > div:first-child:after{
    content:'●';
    font-size: 10px;
    margin-left: 5px;
    line-height: 5px;
    vertical-align: top;
    line-height: 20px;
  }
</style>
