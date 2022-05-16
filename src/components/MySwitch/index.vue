<template>
  <div>
    <img :src="imgSrc" @click="handleClick" :width="width+'px'" :height="height+'px'">
    <div style="text-align: center;font-size: 10px">
      {{name}}
    </div>
  </div>
</template>
<script>

export default {
  name: 'MySwitch',
  data() {
    return {
      imgSrc: '',
      curState: ''
    }
  },
  props: {
    initState: {type: Number, default: 0},
    imgArr: {type: Array},
    width: {type: Number, default: 100},
    height: {type: Number, default: 100},
    name: {type: String, default: 'Name'}
  },
  watch: {
    initState(oldVal, newVal) {
      this.curState = newVal
      this.imgSrc = this.imgArr[this.curState ? 1 : 0]
    }
  },
  created() {
    this.curState = this.initState
    this.imgSrc = this.imgArr[this.initState]
    console.log(this.imgSrc)
  },
  methods: {
    handleClick(e) {
      this.curState = !this.curState
      this.imgSrc = this.imgArr[this.curState ? 1 : 0]
      this.$emit('change-state', this.curState)
    }
  }
}
</script>
