<template>
  <button 
  v-on="$listeners"
  :style="`width:${width}px; height:${height}px`"
  class="l-btn ma-1 rounded">
    <span
    :style="`width:${width}px; height:${height}px`"
    class="l-btn-shadow d-flex rounded"></span>
    <span 
    :style="`width:${width}px; height:${height}px`"
    class="l-btn-base d-flex rounded"></span>
    <span 
    :style="`width:${width}px; height:${height}px`"
    class="l-btn-top d-flex align-center justify-center 
    text-work-san f-16 rounded"><slot/></span>
  </button>
</template>

<script>
export default {
  name:"Button",
  props:{
    width: {
      type: String,
      default: '60',
    },
    height: {
      type: String,
      default: '40',
    },
  },
}
</script>

<style scoped>
.l-btn{
  position: relative;
  border: none;
  background: transparent;
  padding: 0;
  cursor: pointer;
  outline-offset: 4px;
  transition: filter 250ms;
}
.l-btn-shadow{
  position: absolute;
  top: 0;
  left: 0;
  border-radius: 12px;
  background: hsl(0deg 0% 0% / 0.25);
  will-change: transform;
  transform: translate(2px, 2px);
  transition:
    transform
    600ms
    cubic-bezier(.3, .7, .4, 1);
  }
.l-btn-base{
  position: absolute;
  top: 0;
  left: 0;
  border-radius: 12px;
  background: linear-gradient(
    to left,
    rgb(32, 32, 32) 0%,
    rgb(88, 88, 88) 8%,
    rgb(88, 88, 88) 92%,
    rgb(32, 32, 32) 100%
  );
}
.l-btn-top{
  display: block;
  position: absolute;
  top:0;
  left:0;
  border-radius: 12px;
  font-size: 1.25rem;
  color:rgb(32, 32, 32);
  border:2px solid rgb(88, 88, 88);
  background: white;
  will-change: transform;
  transform: translate(-2px, -2px);
  transition:
    transform
    600ms
    cubic-bezier(.3, .7, .4, 1);
  }
.l-btn:hover{
  filter: brightness(110%);
}
.l-btn:hover .l-btn-top{
  transform: translate(-4px, -4px);
  transition:
    transform
    250ms
    cubic-bezier(.3, .7, .4, 1.5);
}
.l-btn:active .l-btn-top{
  transform: translate(0 , 0);
  transition: transform 34ms;
}
.l-btn:hover .l-btn-shadow{
  transform: translate(4px, 4px);
    transition:
      transform
      250ms
      cubic-bezier(.3, .7, .4, 1.5);
}
.l-btn:active .l-btn-shadow{
  transform: translateY(1px);
  transition: transform 34ms;
}
.l-btn:focus:not(:focus-visible) {
    outline: none;
  }
.f-16{
  font-size: 24px;
}
</style>