<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center">
    <div class="d-flex pa-15">
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
          class="option pa-0 ma-3" 
          :class="selected==idx?'blink':null"
          @click="selected=idx">
            <v-card outlined class="transparent pt-3">
              <div class="d-flex align-center justify-center">
                <img :src="option.emoji" width="50%"/>
              </div>
              <!-- keyboard option -->
              <div class="d-flex ma-2">
                <v-card flat class="white black--text px-2 mr-2 rounded-sm">
                  <b class="text-work-san f-16">{{String.fromCharCode(65+idx)}}</b>
                </v-card>
                <p class="text-work-san f-13 mb-0" v-text="option.name"></p>
              </div>
            </v-card>
            <div v-if="selected==idx" class="d-flex align-start justify-end selected">
              <v-icon color="black">mdi-check</v-icon>
            </div>
          </div>
        </div>
        <v-btn :light="dark" :dark="!dark" class="mt-3">
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
    no: String,
    question: String,
    questionDesc: String,
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
        emoji:'/_nuxt/assets/rates/rate1.png',
        rate:1,
        name:'Very Unsatisfied'
      },{
        emoji:'/_nuxt/assets/rates/rate2.png',
        rate:2,
        name:'Slightly Unsatisfied'
      },{
        emoji:'/_nuxt/assets/rates/rate3.png',
        rate:3,
        name:'Neutral'
      },{
        emoji:'/_nuxt/assets/rates/rate4.png',
        rate:4,
        name:'Satisfied'
      },{
        emoji:'/_nuxt/assets/rates/rate5.png',
        rate:5,
        name:'Extremely Satisfied'
      }]
    }
  }
}
</script>

<style scoped>
.option{
  border: 2px solid white;
  border-radius: 5px;
  position: relative;
  max-width: 15vw;
  transition: all 200ms ease-in-out;
}
.option img{
  opacity: 0.5;
  filter: blur(4px);
  transition: all 200ms ease-in-out;
}
.option:hover{
  max-width: 17vw;
}
.option:hover img{
  opacity: 1;
  filter: blur(0);
}
.selected{
  top:-1px;
  right:-1px;
  height:48px;
  width: 48px;
  border-radius: 5px;
  position: absolute;
  background: white;
  clip-path: polygon(0% 0, 100% 0, 100% 100%);
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
</style>