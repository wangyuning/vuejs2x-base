<template>
  <div>
    <!-- 移动动画 start-->
    <div class="box demo1"></div>
    <!-- 移动动画 end-->
    <!-- 翻书，翻页等等动画 start -->
    <div class="demo2">
      <div class="content">
        <div :key="index"
             :class="value.classname"
             v-for="(value, index) in options">
          {{index}}
        </div>
      </div>
    </div>
    <div class="operation">
      <Button @click="prev">上一个</Button>
      <Button @click="next">下一个</Button>
    </div>
  </div>
  <!-- 翻书，翻页等等动画 end -->
</template>
<script>
export default {
  data () {
    return {
      idx: 0,
      options: [
        { classname: 'page ani2' },
        { classname: 'page' },
        { classname: 'page' },
        { classname: 'page' },
        { classname: 'page' }
      ]
    }
  },
  methods: {
    prev: function () {
      if (this.idx === 0) {
        return
      }
      this.options[this.idx].classname = 'page'
      this.idx--
      this.options[this.idx].classname = 'page ani2'
    },
    next: function () {
      if (this.idx === this.options.length - 1) {
        return
      }
      // debugger
      this.options[this.idx].classname = 'page ani1'
      this.idx++
      this.options[this.idx].classname = 'page ani2'
    }
  }
}
</script>

<style lang="less" scoped>
.box {
  height: 100px;
  width: 100px;
  background: #000;
  &.demo1 {
    &:hover {
      transform: translateX(500px);
    }
    // 属性 持续时间 时间函数 延迟触发时间
    transition: transform 1s linear 0.1s;
  }
}
.demo2 {
  -webkit-perspective: 800; // 设置 3D 元素距视图的距离，以像素计；perspective的定义要在其他3d变幻之前，否则无效
  perspective-origin: 50% 50%; // 设置视角位置
  overflow: hidden;
  .content {
    position: relative;
    width: 400px;
    height: 400px;
    transform-style: preserve-3d; // 设置后面的动画都是3D动画
    margin: 0 auto;
    .page {
      position: absolute;
      height: 360px;
      width: 360px;
      padding: 20px;
      background-color: #000;

      color: white;
      font-size: 360px;
      font-weight: bold;
      line-height: 360px;
      text-align: center;

      transform-origin: bottom; // 设置旋转中心或者旋转轴
      transform: rotateX(90deg);
      transition: transform 1s linear;

      &.ani1 {
        transform: rotateX(-90deg);
      }
      &.ani2 {
        transform: rotateX(0deg);
      }
    }
  }
}
</style>
