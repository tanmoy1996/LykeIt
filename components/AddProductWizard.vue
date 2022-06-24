<template>
  <v-card flat class="transparent form-full-screen formBack">
    <v-progress-linear 
    color="grey lighten-2"
    height="7"
    :value="completed()"/>
    <v-card id="questions"
      height="100%" flat class="transparent">
      
      <!-- <Rating class="q" no="4"
      question="How was your expirence"
      questionDesc="What personal need is it solving? How is is helping?" 
      dark/> -->
      <!-- <Range class="q" no="5" 
      question="First off, are you using the product for business or personal use?" 
      range="5"
      dark
      required/> -->
      <!-- <Bool class="q" no="3" 
      question="You are daily using our product." 
      dark
      required/> -->
      <Mcq class="q" no="7" v-model="q2"
      question="First off, are you using the product for business or personal use?" 
      :options="[{
        pic:'/_nuxt/assets/home.png',
        name:'Personal',
        value:'personal',
        },{
        pic:'/_nuxt/assets/building.png',
        name:'Business',
        value:'business',
      },]"
      dark
      multiple
      required/> 
      <Short class="q" no="1" v-model="q1"
      question="Okay. How exactly are you using it?"
      questionDesc="What personal need is it solving? How is is helping?" 
      dark
      required/>
      <!-- 
      <Short class="q" no="2"
      question="Okay. How exactly are you using it?"
      questionDesc="What personal need is it solving? How is is helping?" 
      dark
      email
      required/>
      <Range class="q" no="6"
      question="First off, are you using the product for business or personal use?" 
      range="36"
      dark
      required/>
      
      <Mcq class="q" no="8"
      question="First off, are you using the product for business or personal use?" 
      :options="[{
        pic:require('@/assets/home.png'),
        name:'Personal',
        value:'personal',
        },{
        pic:require('@/assets/building.png'),
        name:'Business',
        value:'business',
      },{
        pic:require('@/assets/home.png'),
        name:'Personal',
        value:'personal',
        },{
        pic:require('@/assets/building.png'),
        name:'Business',
        value:'business',
      },{
        pic:require('@/assets/building.png'),
        name:'Business',
        value:'business',
      },{
        pic:require('@/assets/building.png'),
        name:'Business',
        value:'business',
      }]"
      dark
      required/>
      <Mcq class="q" no="9"
      question="First off, are you using the product for business or personal use?" 
      :options="[{
        pic:'/_nuxt/assets/home.png',
        name:'Option1',
        value:'Option1',
        },{
        pic:'/_nuxt/assets/home.png',
        name:'Option2',
        value:'Option2',
      },{
        pic:'/_nuxt/assets/home.png',
        name:'Option3',
        value:'Option3',
      },{
        pic:'/_nuxt/assets/home.png',
        name:'Option4',
        value:'Option4',
      },{
        pic:'/_nuxt/assets/home.png',
        name:'Option5',
        value:'Option5',
        },{
        pic:'/_nuxt/assets/home.png',
        name:'Option6',
        value:'Option6',
      },{
        pic:'/_nuxt/assets/home.png',
        name:'Option7',
        value:'Option7',
      },{
        pic:'/_nuxt/assets/home.png',
        name:'Option8',
        value:'Option8',
      },{
        pic:'/_nuxt/assets/home.png',
        name:'Option9',
        value:'Option9',
      }]"
      dark
      required/>
      <Mcq class="q" no="10"
      question="First off, are you using the product for business or personal use?" 
      :options="[{
        name:'Personal',
        value:'personal',
        },{
        name:'Business',
        value:'business',
      },{
        name:'Personal',
        value:'personal',
        },{
        name:'Business',
        value:'business',
      },]"
      dark
      required/> 
      <Mcq class="q" no="11" multiple
      question="First off, are you using the product for business or personal use?" 
      :options="[{
        name:'Option1',
        value:'Option1',
        },{
        name:'Option2',
        value:'Option2',
      },{
        name:'Option3',
        value:'Option3',
      },{
        name:'Option4',
        value:'Option4',
      },{
        name:'Option5',
        value:'Option5',
        },{
        name:'Option6',
        value:'Option6',
      },{
        name:'Option7',
        value:'Option7',
      },{
        name:'Option8',
        value:'Option8',
      }]"
      dark
      required/> -->
    </v-card>
    <div id="moveBtn">
      <div class="absBtn">
        <v-btn 
        fab 
        small 
        :disabled="step==0"
        @click="next(false)">
          <v-icon>mdi-arrow-up-thick</v-icon>
        </v-btn>
        <v-btn 
        fab 
        small 
        :disabled="step==questionNos-1"
        @click="next(true)">
          <v-icon>mdi-arrow-down-thick</v-icon>
        </v-btn>
      </div>
    </div>
  </v-card>
</template>

<script>
import Short from './questions/Short.vue';
import Rating from './questions/Rating.vue';
import Mcq from './questions/Mcq.vue';
import Bool from './questions/Bool.vue';
import Range from './questions/Range.vue';


export default {
    name: "AddProduct",
    components: { Short, Rating, Mcq, Bool, Range},
    data() {
        return {
            q1:'',
            q2:'',
            step:0,
            questionNos:10,
        };
    },
    methods: {
      completed(){
        return (this.step/this.questionNos*100);
      },
      next(go) {
        var el = document.querySelector('#questions');
        var questions = el.querySelectorAll('.q')
        this.questionNos=questions.length;
        if(go){
          questions[this.step].classList.toggle('hideStep');
          this.step++;
        }
        else{
          this.step--;
          questions[this.step].classList.toggle('hideStep');
        }  
          console.log("q2", this.q2);   
      },
    },
    
}
</script>

<style scoped>
.form-full-screen{
  height: calc(100vh - 88px);
  position: relative;
  overflow: hidden;
}
.formBack{
  background-color: #052375;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25'%3E%3Cdefs%3E%3ClinearGradient id='a' gradientUnits='userSpaceOnUse' x1='0' x2='0' y1='0' y2='100%25' gradientTransform='rotate(180,683,298)'%3E%3Cstop offset='0' stop-color='%23052375'/%3E%3Cstop offset='1' stop-color='%23031952'/%3E%3C/linearGradient%3E%3Cpattern patternUnits='userSpaceOnUse' id='b' width='300' height='250' x='0' y='0' viewBox='0 0 1080 900'%3E%3Cg fill-opacity='0.03'%3E%3Cpolygon fill='%23444' points='90 150 0 300 180 300'/%3E%3Cpolygon points='90 150 180 0 0 0'/%3E%3Cpolygon fill='%23AAA' points='270 150 360 0 180 0'/%3E%3Cpolygon fill='%23DDD' points='450 150 360 300 540 300'/%3E%3Cpolygon fill='%23999' points='450 150 540 0 360 0'/%3E%3Cpolygon points='630 150 540 300 720 300'/%3E%3Cpolygon fill='%23DDD' points='630 150 720 0 540 0'/%3E%3Cpolygon fill='%23444' points='810 150 720 300 900 300'/%3E%3Cpolygon fill='%23FFF' points='810 150 900 0 720 0'/%3E%3Cpolygon fill='%23DDD' points='990 150 900 300 1080 300'/%3E%3Cpolygon fill='%23444' points='990 150 1080 0 900 0'/%3E%3Cpolygon fill='%23DDD' points='90 450 0 600 180 600'/%3E%3Cpolygon points='90 450 180 300 0 300'/%3E%3Cpolygon fill='%23666' points='270 450 180 600 360 600'/%3E%3Cpolygon fill='%23AAA' points='270 450 360 300 180 300'/%3E%3Cpolygon fill='%23DDD' points='450 450 360 600 540 600'/%3E%3Cpolygon fill='%23999' points='450 450 540 300 360 300'/%3E%3Cpolygon fill='%23999' points='630 450 540 600 720 600'/%3E%3Cpolygon fill='%23FFF' points='630 450 720 300 540 300'/%3E%3Cpolygon points='810 450 720 600 900 600'/%3E%3Cpolygon fill='%23DDD' points='810 450 900 300 720 300'/%3E%3Cpolygon fill='%23AAA' points='990 450 900 600 1080 600'/%3E%3Cpolygon fill='%23444' points='990 450 1080 300 900 300'/%3E%3Cpolygon fill='%23222' points='90 750 0 900 180 900'/%3E%3Cpolygon points='270 750 180 900 360 900'/%3E%3Cpolygon fill='%23DDD' points='270 750 360 600 180 600'/%3E%3Cpolygon points='450 750 540 600 360 600'/%3E%3Cpolygon points='630 750 540 900 720 900'/%3E%3Cpolygon fill='%23444' points='630 750 720 600 540 600'/%3E%3Cpolygon fill='%23AAA' points='810 750 720 900 900 900'/%3E%3Cpolygon fill='%23666' points='810 750 900 600 720 600'/%3E%3Cpolygon fill='%23999' points='990 750 900 900 1080 900'/%3E%3Cpolygon fill='%23999' points='180 0 90 150 270 150'/%3E%3Cpolygon fill='%23444' points='360 0 270 150 450 150'/%3E%3Cpolygon fill='%23FFF' points='540 0 450 150 630 150'/%3E%3Cpolygon points='900 0 810 150 990 150'/%3E%3Cpolygon fill='%23222' points='0 300 -90 450 90 450'/%3E%3Cpolygon fill='%23FFF' points='0 300 90 150 -90 150'/%3E%3Cpolygon fill='%23FFF' points='180 300 90 450 270 450'/%3E%3Cpolygon fill='%23666' points='180 300 270 150 90 150'/%3E%3Cpolygon fill='%23222' points='360 300 270 450 450 450'/%3E%3Cpolygon fill='%23FFF' points='360 300 450 150 270 150'/%3E%3Cpolygon fill='%23444' points='540 300 450 450 630 450'/%3E%3Cpolygon fill='%23222' points='540 300 630 150 450 150'/%3E%3Cpolygon fill='%23AAA' points='720 300 630 450 810 450'/%3E%3Cpolygon fill='%23666' points='720 300 810 150 630 150'/%3E%3Cpolygon fill='%23FFF' points='900 300 810 450 990 450'/%3E%3Cpolygon fill='%23999' points='900 300 990 150 810 150'/%3E%3Cpolygon points='0 600 -90 750 90 750'/%3E%3Cpolygon fill='%23666' points='0 600 90 450 -90 450'/%3E%3Cpolygon fill='%23AAA' points='180 600 90 750 270 750'/%3E%3Cpolygon fill='%23444' points='180 600 270 450 90 450'/%3E%3Cpolygon fill='%23444' points='360 600 270 750 450 750'/%3E%3Cpolygon fill='%23999' points='360 600 450 450 270 450'/%3E%3Cpolygon fill='%23666' points='540 600 630 450 450 450'/%3E%3Cpolygon fill='%23222' points='720 600 630 750 810 750'/%3E%3Cpolygon fill='%23FFF' points='900 600 810 750 990 750'/%3E%3Cpolygon fill='%23222' points='900 600 990 450 810 450'/%3E%3Cpolygon fill='%23DDD' points='0 900 90 750 -90 750'/%3E%3Cpolygon fill='%23444' points='180 900 270 750 90 750'/%3E%3Cpolygon fill='%23FFF' points='360 900 450 750 270 750'/%3E%3Cpolygon fill='%23AAA' points='540 900 630 750 450 750'/%3E%3Cpolygon fill='%23FFF' points='720 900 810 750 630 750'/%3E%3Cpolygon fill='%23222' points='900 900 990 750 810 750'/%3E%3Cpolygon fill='%23222' points='1080 300 990 450 1170 450'/%3E%3Cpolygon fill='%23FFF' points='1080 300 1170 150 990 150'/%3E%3Cpolygon points='1080 600 990 750 1170 750'/%3E%3Cpolygon fill='%23666' points='1080 600 1170 450 990 450'/%3E%3Cpolygon fill='%23DDD' points='1080 900 1170 750 990 750'/%3E%3C/g%3E%3C/pattern%3E%3C/defs%3E%3Crect x='0' y='0' fill='url(%23a)' width='100%25' height='100%25'/%3E%3Crect x='0' y='0' fill='url(%23b)' width='100%25' height='100%25'/%3E%3C/svg%3E");
  background-attachment: fixed;
  background-size: cover;
}
.text-dec{
  font-family: Ubunto;
  font-size: 48px;
  line-height: 1;
  letter-spacing: 3px;
}
.answer-text{
  font-size: 30px;
  line-height: 1;
}
.questionSet{
  transition: all ease-in-out 500ms;
  transform: translateY(0);
}
.absBtn{
  position: absolute;
  bottom:8px;
  right:8px;
  z-index:5;
}
.q{
  opacity: 1;
  transition: all 200ms ease-in-out;
}
.hideStep{
  opacity:0;
  height:0 !important;
}
</style>