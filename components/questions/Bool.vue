<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center">
    <div class="d-flex pa-md-15 pa-5 no-outline" @keypress="key($event)" tabindex="0">
      <span class="mr-1">{{no}}.</span>
      <div>
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <div class="mt-10 ">
          <Button width="250" height="45" class="mb-5" @click="selectAns(0)">
            <p class="text-work-san f-16 mb-0">Yes</p>
          </Button>
          <Button width="250" height="45" class="mb-5" @click="selectAns(1)">
            <p class="text-work-san f-16 mb-0">No</p>
          </Button>
        </div>
        <Button width="85" @click="$emit('next');">
          <div class="d-flex">
            <p class="mb-0 grey--text text--darken-3 f-16">ok</p>
            <v-icon color="grey darken-3" class="ml-2">mdi-arrow-right-thin</v-icon>
          </div>
        </Button>
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  name:"Bool",
  props:{
    value:Boolean,
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
    },
  },
  data(){
    return{
      selected:-1,
    }
  },
  methods:{
    selectAns(idx){
      if(this.selected==idx){
        this.selected=-1;
      }
      else{
        this.selected=idx;
      }
      this.updateValue(this.selected==0)
      setTimeout(()=>{this.$emit('next')}, 400);
    },
    key(e) {
      if(e.key.toLowerCase()=='t'){
      this.selectAns(0);
    }
    else if(e.key.toLowerCase()=='f'){
      this.selectAns(1);
    }
    },
    updateValue(value){
      this.$emit('input',value);
    },
  }
}
</script>
