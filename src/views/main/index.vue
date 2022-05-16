<template>
  <div class="line-block">
    <div class="one">
      <div id="block-one" class="block-one">1</div>
      <div id="block-two" class="block-two">2</div>
    </div>
    <div class="three">
      <el-switch
        v-model="value1"
        class="el-switch__button"
        on-value="1"
        off-value="0"
        active-icon-class="el-icon-success"
        inactive-icon-class="el-icon-error"
        @change="changeSwitch"/>
    </div>
    <div style="display: flex">
      <my-switch
        name="我的阀门"
        :img-arr="[require('@/assets/image/down.gif'),require('@/assets/image/up.gif')]"
        :init-state="probestate"
        :width="100"
        :height="80"
        @change-state="changeMySwitch">
      </my-switch>
    </div>

    <div>
      <my-watcher
        :img-src="require('@/assets/image/watcher_round.png')"
        :watcherNum="initNum">
      </my-watcher>
    </div>
    <div>
      <MyFan >
      </MyFan>
    </div>
  </div>

</template>

<script>
import LeaderLine from 'leader-line'
import MySwitch from '@/components/MySwitch'
import MyWatcher from '@/components/MyWatcher'
import MyFan from '@/components/MyFan'

export default {
  components: { MySwitch, MyWatcher, MyFan },
  data() {
    return {
      value1: false,
      probestate: 0,
      lineContainer: null,
      initNum: 20
    }
  },
  // 注册监听
  mounted() {
    this.getLine()
    this.lineContainer.position()
    setTimeout(() => {
      this.initNum = 50
    }, 0)
    // window.addEventListener('resize', this.getScroll)
  },
  // 销毁监听，防止内存泄露
  destroyed() {
    this.lineContainer.remove()
    // window.removeEventListener('resize', this.getScroll)
  },
  methods: {
    changeMySwitch(data) {
      console.log('------------------------------->', data)
    },
    changeSwitch(data) {
      if (data) {
        this.probestate = 0
        this.lineContainer.color = 'blue'
      } else {
        this.probestate = 1
        this.lineContainer.color = 'white'
      }
    },
    getLine() {
      const dom1 = document.getElementById('block-one')
      const dom2 = document.getElementById('block-two')
      const styleOption = {
        color: 'white', // 指引线颜色
        endPlug: 'behind', // 指引线结束点的样式 hand,disc
        size: 20, // 线条尺寸
        startSocket: 'left', // 在指引线开始的地方从元素左侧开始
        endSocket: 'right', // 在指引线开始的地方从元素右侧结束
        outline: true,
        path: 'straight', // straight,arc,fluid,magnet,grid
        dash: {
          // 虚线样式
          animation: true // 让线条滚动起来
        }
      }
      console.log(LeaderLine)
      this.lineContainer = new LeaderLine(dom1, dom2, styleOption)
    }
  }
}
</script>

<style lang="scss" scoped>
.line-block {
  height: 90vh;

  .one {
    display: flex;
    justify-content: space-around;
    // height: 100px;
  }

  .block-one {
    border: 1px solid blue;
    padding: 10px;
  }

  .block-two {
    border: 1px solid blue;
    padding: 10px;
  }

}

</style>
