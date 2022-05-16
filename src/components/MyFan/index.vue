<template>
  <div class="myFan" :style="{width:width+'px',height:height+'px'}">
    <div class="fans">
      风扇
    </div>
    <div class="data">
      <div >
        PWM:{{ fanSpeed }}
      </div>
      <div >
        转 速:{{ fanSpeed }}
      </div>
    </div>
  </div>
</template>
<script>

export default {
  name: 'MyFan',
  data() {
    return {
      speed: ''
    }
  },
  props: {
    fanPwm: { type: Number, default: 0 },
    fanSpeed: { type: Number, default: 0 },
    width: { type: Number, default: 160 },
    height: { type: Number, default: 80 }
  },
  watch: {
    fanSpeed(newVal) {
    }
  }
}
</script>

<style>
.myFan {
  border: 1px solid #000000;
}
.fans{
  border: 1px solid #000000;
  float: left;
}
.data{
  border: 1px solid #000000;
float: right;
}
</style>

