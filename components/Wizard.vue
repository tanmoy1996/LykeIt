<template>
  <v-card tile flat class=" form-full-screen">
    <!-- <div class="background">
      <div class="whiteGrad"> -->
        <v-progress-linear 
          color="grey "
          height="7"
          :value="completed()"/>
        <v-card id="questions" flat class="transparent form-full-screen" >
          <!-- <l-bubble class="q" :dark="dark" no="1" v-model="q6" @next="next(true)"
            question="Features you like the most?" 
            required/> -->
            <l-short class="q" :dark="dark" no="1" email v-model="q1" @next="next(true)"
              question="Please enter your email?"
              questionDesc="Your response will be stored in our system?" 
              required/>
            <l-bool class="q" :dark="dark" keyboardSelect no="2" v-model="q2" @next="next(true)"
            question="Are you using Godial?" 
            questionDesc="Godial is a TeleCalling CRM software?" 
            required/>
            <l-rating class="q" :dark="dark" no="1" v-model="q3" @next="next(true)"
            question="How is your expirence using Godial?"/>
            <l-mcq class="q" :dark="dark" :keyboardSelect="false" no="5" v-model="q5" @next="next(true)"
              question="Which feature you use the most in Godial?" 
              :options="features"
              multiple
              required/> 
            <l-range class="q" :dark="dark" no="3" v-model="q4" @next="next(true)"
            question="By what percentage have godial helped your lead management?"
            questionDesc="You can select by dragging the thumb" 
            range="100"
            required/>
            
        </v-card>
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
        <!-- </div>
      </div> -->
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
              { name: 'CRM' },
              { name: 'Pipeline' },
              { name: 'Automation' },
              { name: 'Broadcast Survey' },
              { name: 'Leaderboard' },
              { name: 'Forms Integration' },
              // { pic:require('@/assets/home.png'), name: 'Forms Integration' }
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
.background{
  background-image: url('@/assets/topo.svg');
  background-repeat: repeat;
}
.whiteGrad{
  background: rgb(255,255,255);
  background: linear-gradient(45deg, rgba(255,255,255,1) 0%, rgba(255,255,255,1) 48%, rgba(255,255,255,0) 100%);
}
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