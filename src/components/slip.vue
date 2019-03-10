<template>
  <div class="slip"
       @touchstart='handleTouchstart'
       @touchend='handleTouchend'>
  </div>
</template>

<script>
export default {
  data () {
    return {

    }
  },
  methods: {
    handleTouchstart (e) {
      e.preventDefault();
      this.startX = e.touches[0].pageX;
      this.startY = e.touches[0].pageY;
    },
    handleTouchend (e) {
      e.preventDefault();
      this.endX = e.changedTouches[0].pageX;
      this.endY = e.changedTouches[0].pageY;
      this.handleUpOrDown(this.startX, this.startY, this.endX, this.endY);
    },
    handleUpOrDown (startX, startY, endX, endY) {
      let direction = this.handleGetSlideDirection(startX, startY, endX, endY);
      switch (direction) {
        case 0:
          // console.log("没滑动");
          break;
        case 1:
          // console.log("向上");
          this.$emit('handleup')
          break;
        case 2:
          // console.log("向下");
          this.$emit('handledown')
          break;
        case 3:
          // console.log("向左");
          this.$emit('handleleft')
          break;
        case 4:
          // console.log("向右");
          this.$emit('handleright')
          break;
        default:
          break;
      }
    },
    //根据起点和终点返回方向 1：向上，2：向下，3：向左，4：向右,0：未滑动
    handleGetSlideDirection (startX, startY, endX, endY) {
      let dy = startY - endY;
      let dx = endX - startX;
      let result = 0;
      //如果滑动距离太短
      if (Math.abs(dx) < 2 && Math.abs(dy) < 2) {
        return result;
      }
      let angle = this.handleGetSlideAngle(dx, dy);
      if (angle >= -45 && angle < 45) {
        result = 4;
      } else if (angle >= 45 && angle < 135) {
        result = 1;
      } else if (angle >= -135 && angle < -45) {
        result = 2;
      }
      else if ((angle >= 135 && angle <= 180) || (angle >= -180 && angle < -135)) {
        result = 3;
      }
      return result;
    },
    //返回角度
    handleGetSlideAngle (dx, dy) {
      return Math.atan2(dy, dx) * 180 / Math.PI;
    },
  },
}
</script>

<style lang='scss' scoped>
.slip {
  height: 100%;
  width: 100%;
}
</style>