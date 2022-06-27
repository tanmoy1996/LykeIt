<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center">
    <div class="d-flex pa-md-15 pa-5 no-outline">
      <span class="mr-1">{{no}}.</span>
      <div>
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <div id="bub" class="bubble" @click="wobble">
          <!-- <div class="drop"></div> -->
          <h4>Simple Text</h4>            
        </div>
          <!-- <v-btn :light="dark" :dark="!dark" class="mt-3" @click="$emit('next');">
            OK
            <v-icon right>mdi-check</v-icon>
          </v-btn> -->
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  name:"Bubble",
  props:{
    value:Boolean,
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
    },
  },
  data(){
    return{
      selected:[],
    }
  },
  methods:{
    wobble(){
      var bub = document.querySelector('#bub');
      // bub.classList.add("bubble-pop");
      bub.classList.add("bubble-wobble");
      setTimeout(()=>{bub.classList.remove("bubble-wobble");}, 600);
    },
    updateValue(value){
      this.$emit('input',value);
    },
  }
}
</script>

<style scoped>
.bubble{
  width:100px;
  height:100px;
  border-radius: 50%;
  background: #3e6bff;
  color:white;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: float 6s ease-in-out infinite;
  }
/* .drop {
  position: absolute;
  height: 100px;
  width: 100px;
  background: #54ABFB;
  border-radius: 50%;
  opacity: 0.8;
  border: 2px solid #3d93ff;
  transition: all cubic-bezier(0,-2.28, 1, 2.67) 100ms;
}
.drop::before {
  content:'';
  position: absolute;
  height: 100%;
  width: 100%;
  background: #318CFE;
  border-radius: 50%;
  box-shadow: inset -6px 6px 10px #1B6CFB, inset 2px 6px 10px #1a74e5, inset 20px -20px 22px white, inset 40px -40px 44px #a8ceff;
}
.drop::after {
  content: "";
  position: absolute;
  height: 20px;
  width: 20px;
  background: #E6FDFB;
  border-radius: 44% 56% 46% 54% / 36% 50% 50% 64%;
  right: 10%;
  top: 22%;
  box-shadow: 16px 40px 0 -10px white;
  opacity: 0.8;
} */
.bubble h4{
  z-index: 5;
}

.bubble-wobble {
-webkit-animation: bubbleWobble 0.5s ease;
-moz-animation: bubbleWobble 0.5s ease;
animation: bubbleWobble 0.5s ease;
}
@-webkit-keyframes bubbleWobble {
0% {
-webkit-transform: scale(1);
}
20% {
-webkit-transform: scale(0.8);
}
40% {
-webkit-transform: scale(1.1);
}
60% {
-webkit-transform: scale(0.95);
} 
80% {
-webkit-transform: scale(1.03);
} 
100% {
-webkit-transform: scale(1);
} 
}
@-moz-keyframes bubbleWobble {
0% {
-moz-transform: scale(1);
}
20% {
-moz-transform: scale(0.8);
}
40% {
-moz-transform: scale(1.1);
}
60% {
-moz-transform: scale(0.95);
} 
80% {
-moz-transform: scale(1.03);
} 
100% {
-moz-transform: scale(1);
} 
}
@keyframes bubbleWobble {
0% {
transform: scale(1);
}
20% {
transform: scale(0.8);
}
40% {
transform: scale(1.1);
}
60% {
transform: scale(0.95);
} 
80% {
transform: scale(1.03);
} 
100% {
transform: scale(1);
} 
}

.bubble-pop {
-webkit-animation: bubblePop 0.4s ease;
-moz-animation: bubblePop 0.4s ease;
animation: bubblePop 0.4s ease;
opacity: 0;
}
@-webkit-keyframes bubblePop {
0% {
-webkit-transform: scale(1);
opacity: 1;
}
20% {
-webkit-transform: scale(0);
opacity: 0.6;
}
100% {
-webkit-transform: scale(0.5);
opacity: 0;
}
}
@-moz-keyframes bubblePop {
0% {
-moz-transform: scale(1);
opacity: 1;
}
20% {
-moz-transform: scale(0);
opacity: 0.6;
}
100% {
-moz-transform: scale(0.5);
opacity: 0;
}
}
@keyframes bubblePop {
0% {
transform: scale(1);
opacity: 1;
}
20% {
transform: scale(0);
opacity: 0.6;
}
100% {
transform: scale(0.5);
opacity: 0;
}
}

@keyframes float {
	0% {
		box-shadow: 0 5px 15px 0px rgba(0,0,0,0.6);
		transform: translatey(0px);
	}
	50% {
		box-shadow: 0 25px 15px 0px rgba(0,0,0,0.2);
		transform: translatey(-20px);
	}
	100% {
		box-shadow: 0 5px 15px 0px rgba(0,0,0,0.6);
		transform: translatey(0px);
	}
}
</style>