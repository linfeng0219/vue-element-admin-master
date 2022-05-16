<template>
  <div class="watcher" :style="{'background':'url('+imgSrc+') no-repeat left top',width:width+'px',height:height+'px'}">
    <div>
      <div class="title">
        {{ watcherName }}
      </div>
      <div class="num" :style="{'background':curColor,'width':( width - 20 )+'px'}">
        {{ watcherNum }}
      </div>
      <div class="unit">
        {{ watcherUnit }}
      </div>
    </div>
    <div style="text-align: center;font-size: 10px" :style="{bottom:0+'px'}">
      {{ name }}
    </div>
  </div>
</template>
<script>

export default {
  name: 'MyWatcher',
  data() {
    return {
      curColor: ''
    }
  },
  props: {
    imgSrc: {type: String},
    watcherName: {type: String, default: '表名'},
    watcherNum: {type: Number, default: 0},
    watcherUnit: {type: String, default: '单位'},
    warnNum: {type: Number, default: 10},
    normalColor: {type: String, default: '#F19984FF'},
    warnColor: {type: String, default: '#00ffe1'},
    width: {type: Number, default: 70},
    height: {type: Number, default: 123},
    name: {type: String, default: 'Name'}
  },
  watch: {
    num(newVal) {
      if (newVal > this.warnNum) {
        this.curColor = this.warnColor
      } else {
        this.curColor = this.normalColor
      }
    }
  },
  created() {
    this.curColor = this.normalColor
  }
}
</script>
<style>
.watcher {
  -webkit-box-flex: 1;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-box-align: center;
  -webkit-box-pack: justify;
  justify-content: space-between;
  flex-direction: column;
}

.title {
  font-size: 10px;
  text-align: center;
  margin-top: 12px;
}

.num {
  border: 1px solid #000000;
  height: 20px;
  font-size: 10px;
  margin: 0 auto;
  text-align: center;
  line-height: 20px;
}

.unit {
  font-size: 10px;
  text-align: center;
}
</style>
