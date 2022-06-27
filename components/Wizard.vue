<template>
  <v-card flat class=" form-full-screen">
    <v-img :src="background" class="back">
      <v-progress-linear 
      color="grey "
      height="7"
      :value="completed()"/>
      <v-card id="questions" flat class="transparent form-full-screen" >
        <l-bubble class="q" :dark="dark" no="1" v-model="q6" @next="next(true)"
          question="Features you like the most?" 
          required/>
        <l-mcq class="q" :dark="dark" :keyboardSelect="false" no="5" v-model="q5" @next="next(true)"
          question="Which feature you use the most in Godial?" 
          :options="features"
          multiple
          required/> 
          <l-short class="q" :dark="dark" no="1" v-model="q1" @next="next(true)"
          question="Are you using Godial?"
          questionDesc="It Godial helping you to getting your Leads?" 

          required/>
          <l-rating class="q" :dark="dark" no="3" v-model="q3" @next="next(true)"
          question="How is your expirence using Godial?"
          />
          <l-bool class="q" :dark="dark" keyboardSelect no="2" v-model="q2" @next="next(true)"
          question="Can you let us know your experience using Godial?" 

          required/>
          <l-range class="q" :dark="dark" no="4" v-model="q4" @next="next(true)"
          question="On a mark of 1 to 10 how will you rate Godial? 10 being happy and 1 means sad." 
          range="10"
          required/>
          <l-range class="q" :dark="dark" no="4" v-model="q4" @next="next(true)"
          question="On a mark of 1 to 10 how will you rate Godial? 10 being happy and 1 means sad." 
          range="50"
          required/>
          
      </v-card>
    </v-img>
      <div class="absBtn">
        <v-btn 
        :dark="!dark"
        fab 
        small 
        :disabled="step==0"
        @click="next(false)">
          <v-icon>mdi-arrow-up-thick</v-icon>
        </v-btn>
        <v-btn 
        :dark="!dark"
        fab 
        small 
        :disabled="step==questionNos-1"
        @click="next(true)">
          <v-icon>mdi-arrow-down-thick</v-icon>
        </v-btn>
      </div>

  </v-card>
</template>

<script>
import {LShort, LRating, LMcq, LBool, LRange, LBubble} from './questions'

export default {
    name: "AddProduct",
    components: { LShort, LRating, LMcq, LBool, LRange, LBubble},
    props:{
      dark:false,
      background:'',
  },
    data() {
        return {
            q1:'',
            q2:'',
            q3:'',
            q4:'',
            q5:'',
            q6:'',
            features:[
              { pic:require('@/assets/home.png'), name: 'CRM' },
              { pic:require('@/assets/home.png'), name: 'Pipeline' },
              { pic:require('@/assets/home.png'), name: 'Automation' },
              { pic:require('@/assets/home.png'), name: 'Broadcast Survey' },
              { pic:require('@/assets/home.png'), name: 'Leaderboard' },
              { pic:require('@/assets/home.png'), name: 'Forms Integration' }
            ],
            step:0,
            questionNos:5,
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
        if(go && this.step!=this.questionNos-1){
          questions[this.step].classList.toggle('hideStep');
          this.step++;
        }
        else if(!go){
          this.step--;
          questions[this.step].classList.toggle('hideStep');
        }   
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
#questions{
  z-index:3;
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