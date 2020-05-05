<template>
  <div id="app" ref="dC" v-on="listeners">
    <HelloWorld :animate="animate" />
    <HelloWorld :animate="animate" />
    <!-- <HelloWorld /> -->
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld
  },
  data() {
    return {
      x: Number,
      y: Number,
      limit: Number,
      currentLimit: Number,
      isDrawing: Number,
      show: true,
      rotateValue: 0,
      rotateDeg: 0,
      animate: { x: 0, y: 0, x1: 0, y1: 0, rotateDeg: 0 }
    };
  },
  computed: {
    listeners() {
      return {
        touchstart: this.mouseDown,
        touchend: this.touchUp,
        touchmove: this.mouseMove,
        mousedown: this.mouseDown,
        mousemove: this.mouseMove,
        mouseup: this.mouseUp
      };
    }
  },
  methods: {
    mouseDown(e) {
      if (e instanceof TouchEvent) {
        const touchobj = e.changedTouches[0];
        this.x = touchobj.pageX;
        this.y = touchobj.pageY;
        this.isDrawing = true;
      } else {
        this.x = e.offsetX;
        this.y = e.offsetY;
        this.isDrawing = true;
      }
    },
    mouseMove(e) {
      if (e instanceof TouchEvent) {
        // const touchobj = e.changedTouches[0];
        if (this.isDrawing === true) {
          this.currentLimit = 0;
        }
      } else {
        if (this.isDrawing === true) {
          this.currentLimit = e.offsetX;
        }
      }
    },
    mouseUp(e) {
      if (this.isDrawing === true) {
        // console.log(this.swipeTigger(e.offsetX, e.offsetY));
        this.animate = { x: this.x, y: this.y, x1: e.offsetX, y1: e.offsetY };
        this.x = 0;
        this.y = 0;
        this.currentLimit = 0;
        this.isDrawing = false;
      }
    },
    touchUp(e) {
      if (e instanceof TouchEvent) {
        const touchobj = e.changedTouches[0];
        if (this.isDrawing === true) {
          // console.log(this.swipeTigger(e.offsetX, e.offsetY));
          const dist = Math.abs(touchobj.pageX - this.x); // get total dist traveled by finger while in contact with surface // check that elapsed time is within specified, horizontal dist traveled >= threshold, and vertical dist traveled <= 100
          // elapsedTime = new Date().getTime() - startTime
          // get time elapsed
          var swiperightBol = dist >= 150;
          if (swiperightBol) {
            this.animate = {
              x: this.x,
              y: this.y,
              x1: touchobj.pageX,
              y1: touchobj.pageY
            };
          }
          this.x = 0;
          this.y = 0;
          this.currentLimit = 0;
          this.isDrawing = false;
        }
      }
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  // margin-top: 60px;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
body {
  margin: 0px;
}
</style>
