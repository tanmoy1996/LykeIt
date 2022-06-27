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
          <div v-for="(option,idx) of options" 
          flat 
          :key="idx" 
          class="option pa-0 ma-md-3 mr-2 mb-2" 
          :class="`${selected==idx?'blink':null} option${dark?'Dark':'Light'}`"
          @click="select(idx)">
            <v-card outlined class="transparent pt-3">
              <div class="d-flex align-center justify-center">
                <img :src="option.emoji" 
                width="50%" 
                :class="selected==idx?'no-blur':null"/>
              </div>
              <!-- keyboard option -->
              <div class="d-flex ma-2">
                <v-card v-if="keyboardSelect" flat class="white black--text px-2 mr-2 rounded-sm">
                  <b class="text-work-san f-16">{{String.fromCharCode(65+idx)}}</b>
                </v-card>
                <p class="text-work-san f-13 mb-0" v-text="option.name"></p>
              </div>
            </v-card>
            <div v-if="selected==idx" class="d-flex align-start justify-end selected"
            :class="dark?'white':'grey darken-4'">
              <v-icon :color="dark?'black':'white'">mdi-check</v-icon>
            </div>
          </div>
        </div>
        <v-btn :light="dark" :dark="!dark" class="mt-md-3 mt-0" @click="$emit('next');">
          OK
          <v-icon right>mdi-check</v-icon>
        </v-btn>
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  name:"Rating",
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
      setTimeout(()=>{this.$emit('next')}, 1000);
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
.option{
  border-radius: 5px;
  position: relative;
  width: max(180px,15vw);
  cursor: pointer;
  transition: all 200ms ease-in-out;
}
.option img{
  opacity: 0.5;
  filter: blur(4px);
  transition: all 200ms ease-in-out;
}
.option:hover{
  width: max(200px,17vw);
}
.option:hover img{
  opacity: 1;
  filter: blur(0);
}
.optionLight{
  border: 2px solid rgb(65, 65, 65);
}
.optionDark{
  border: 2px solid white;
}
.selected{
  top:-1px;
  right:-1px;
  height:48px;
  width: 48px;
  border-radius: 5px;
  position: absolute;
  clip-path: polygon(0% 0, 100% 0, 100% 100%);
}
.no-blur{
  opacity: 1 !important;
  filter: blur(0) !important;
}
.f-13{
  font-size: 13px;
}
.blink {
  animation: blinker 500ms linear 2;
}

@keyframes blinker {
  0% {
    border: 2px solid white;
  }
  33% {
    border: 2px solid rgb(54, 54, 54);
  }
  66% {
    border: 2px solid white;
  }
}

@media (max-width: 480px) {
  .option{
  width: 100px;
  }
  .option:hover{
  width: 100px;
}
  .option img{
    filter: blur(0);
    transition: all 200ms ease-in-out;
  }
  .f-13{
  display: none;
}
}
</style>