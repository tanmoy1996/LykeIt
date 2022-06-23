<template>
  <v-card height="100%" flat :dark="dark" class="transparent d-flex align-center">
    <div class="d-flex pa-15">
      <span class="mr-1">{{no}}.</span>
      <div>
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <v-text-field 
        :dark="dark" 
        :placeholder="email?'name@example.com':'Type your answer here...'" 
        class="text-work-san answer"/>
        <div class="d-flex  align-center">
          <v-btn :light="dark" :dark="!dark" class="mr-2">
            OK
            <v-icon right>mdi-check</v-icon>
          </v-btn>
          <p class="text-caption mb-0">press <b>Enter</b>
          <v-icon small>mdi-arrow-left-bottom</v-icon>
          </p>
        </div>
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  name:"Short",
  props:{
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

</style>