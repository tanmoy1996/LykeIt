<template>
  <v-card height="100%" flat :dark="dark" class="transparent d-flex align-center">
    <div class="d-flex pa-md-15 pa-5">
      <span class="mr-1">{{no}}.</span>
      <div>
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <v-text-field 
        :dark="dark"
        :placeholder="email?'name@example.com':'Type your answer here...'" 
        class="text-work-san answer"
        :value="value"
        @input="updateValue($event)"/>
        <div class="d-flex  align-center">
          <v-btn :light="dark" :dark="!dark" class="mr-2" @click="$emit('next');">
            OK
            <v-icon right>mdi-check</v-icon>
          </v-btn>
        </div>
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  name:"Short",
  props:{
    value:String,
    no: String,
    question: String,
    questionDesc: String,
    dark: {
      type: Boolean,
      default: false,
    },
    email: {
      type: Boolean,
      default: false
    },
    required: {
      type: Boolean,
      default: false
    }
  },
  data(){
    return{
      ans:'',
    }
  },
  methods:{
    updateValue(value){
      this.$emit('input',value);
    }
  }
}
</script>

<style >
.answer{
  font-size:28px;
}
.answer .v-input__slot {
  padding: 10px 0;
}
@media (max-width: 480px) {
  .answer{
  font-size:18px;
  }
}
</style>