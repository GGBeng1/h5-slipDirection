<template>
  <div class="home">
    <div class="box">
      <slip-direction @handleup='handleup' @handledown="handledown" @handleleft='handleleft' @handleright='handleright'>
      </slip-direction>
    </div>
    <span>滑动方向：<span class="text">{{direction}}</span></span>
  </div>
</template>

<script>
import SlipDirection from "@/components/slip.vue"
export default {
  name: 'home',
  components: {
    SlipDirection
  },
  data () {
    return {
      direction: "请务必在移动端设备或模拟器下滑动"
    }
  },
  methods: {
    handleup () {
      this.direction = "向上"
    },
    handledown () {
      this.direction = "向下"
    },
    handleleft () {
      this.direction = "向左"
    },
    handleright () {
      this.direction = "向右"
    },
  },
}
</script>
<style lang="scss" scoped>
.home {
  height: 100%;
  text-align: center;
  .box {
    width: 200px;
    height: 200px;
    background-color: pink;
    margin: 50px auto;
  }
  span {
    margin-top: 20px;
    &.text {
      color: red;
    }
  }
}
</style>
