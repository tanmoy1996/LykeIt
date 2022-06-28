<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center">
    <div class="d-flex pa-md-15 pa-5 no-outline" @keypress="key($event)" tabindex="0">
      <span class="mr-1">{{no}}.</span>
      <div>
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <div class="d-flex flex-wrap">
          <div 
            class="mr-1 mb-1"
            v-for="(option,idx) of options" 
            :key="idx" 
            @click="select(idx)">
            <Button width="150" height="110" class="d-sm-block d-none">
              <div class="py-3">
                <img :src="option.emoji" width="50%"/>
                <p class="text-work-san f-13 mb-0" v-text="option.name"></p>
              </div>
            </Button>
            <Button width="50" height="50" class="d-sm-none d-block">
              <div class="py-3">
                <img :src="option.emoji" 
                width="60%" 
                :class="selected==idx?'no-blur':null"/>
                <p class="text-work-san f-13 mb-0" v-text="option.name"></p>
              </div>
            </Button>
            <!-- <v-card outlined class="transparent pt-3">
              <div class="d-flex ma-2">
                <v-card v-if="keyboardSelect" flat class="white black--text px-2 mr-2 rounded-sm">
                  <b class="text-work-san f-16">{{String.fromCharCode(65+idx)}}</b>
                </v-card>
              </div>
            </v-card>
            <div v-if="selected==idx" class="d-flex align-start justify-end selected"
            :class="dark?'white':'grey darken-4'">
              <v-icon :color="dark?'black':'white'">mdi-check</v-icon>
            </div> -->
          </div>
        </div>
        <Button width="85" class="mt-4">
          <div class="d-flex">
            <p class="mb-0 grey--text text--darken-3">ok</p>
            <v-icon color="grey darken-3" class="ml-2">mdi-arrow-right-thin</v-icon>
          </div>
        </Button>
      </div>
    </div>
  </v-card>
</template>

<script>
import Button from '../Button.vue';
export default {
  name:"Rating",
  components: { Button },
  props:{
    value:String,
    no: String,
    question: String,
    questionDesc: String,
    keyboardSelect:{
      type: Boolean,
      default: false,
    },
    dark: {
      type: Boolean,
      default: false,
    },
    required: {
      type: Boolean,
      default: false
    }
  },
  data(){
    return{
      selected:-1,
      options:[{
        emoji:require('@/assets/rates/rate1.png'),
        rate:1,
        name:'Very Unsatisfied'
      },{
        emoji:require('@/assets/rates/rate2.png'),
        rate:2,
        name:'Slightly Unsatisfied'
      },{
        emoji:require('@/assets/rates/rate3.png'),
        rate:3,
        name:'Neutral'
      },{
        emoji:require('@/assets/rates/rate4.png'),
        rate:4,
        name:'Satisfied'
      },{
        emoji:require('@/assets/rates/rate5.png'),
        rate:5,
        name:'Extremely Satisfied'
      }]
    }
  },
  methods:{
    select(idx){
      this.selected=idx
      this.updateValue(`${this.selected+1}`);
      setTimeout(()=>{this.$emit('next')}, 400);
    },
    key(e) {
      var keyPressed  = (e.keyCode<=90?e.keyCode+32:e.keyCode)-97;
      if(keyPressed>0 && keyPressed<6){
        this.select(keyPressed);
      }
      
    },
    updateValue(value){
      this.$emit('input',value);
    }
  }
}
</script>

<style scoped>
.f-13{
  font-size: 13px;
}
@media (max-width: 480px) {
  .f-13{
  display: none;
}
}
</style>