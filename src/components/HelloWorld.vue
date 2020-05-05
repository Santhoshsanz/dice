<template>
  <!-- <main> -->
  <div class="dice-container">
    <!-- <textarea v-model="rotateValue" />
    {{ classObject }} -->
    <transition v-on:before-enter="beforeEnter" v-on:enter="enter">
      <div class="dice" :style="classObject">
        <div class="front diceLayer">
          <span></span>
          <span></span>
          <span></span>
        </div>
        <div class="back diceLayer">
          <!-- <span></span> -->
        </div>
        <div class="right diceLayer">
          <span></span>
        </div>
        <div class="left diceLayer">
          <span></span>
          <span></span>
        </div>
        <div class="top diceLayer">
          <!-- <span></span>
          <span></span>
          <span></span> -->
        </div>
        <div class="bottom diceLayer">
          <!-- <span></span>
          <span></span>
          <span></span>
          <span></span> -->
        </div>
      </div>
    </transition>
  </div>
</template>

<style lang="scss">
.dice-container {
  margin: 60px;
}

main {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.add-keyframe {
  animation-name: rotate;
  animation-iteration-count: 1;
  animation-duration: 3s;
  animation-timing-function: ease-in-out;
  animation-name: opacity;
}
.diceLayer {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}
.dice {
  width: 20px;
  height: 200px;
  position: relative;
  transform-style: preserve-3d;
  transform: rotateX(0deg) rotateY(3600deg) translateX(0);
  animation-iteration-count: 1;
  //  animation-name: rotate;
  animation-duration: 1s;
  animation-timing-function: ease-in-out;
  animation-fill-mode: forwards;
  transform-origin: top center;

  > div {
    height: 200px;
    width: 20px;
    position: absolute;
    background: #f76331;
    border-radius: 2px;
    border: 1px solid #f77d54;
    padding: 1px;
  }

  span {
    width: 8px;
    height: 8px;
    background: #fff;
    border-radius: 50%;
    display: block;
    // position: absolute;
  }

  .front {
    transform: rotateY(0deg) translateZ(10px);
    span {
      &:nth-child(1) {
        top: 10px;
        left: 12px;
      }
      &:nth-child(2) {
        top: 10px;
        right: 12px;
      }
      &:nth-child(3) {
        top: 26px;
        left: 12px;
      }
      &:nth-child(4) {
        top: 26px;
        right: 12px;
      }
      &:nth-child(5) {
        bottom: 10px;
        left: 12px;
      }
      &:nth-child(6) {
        bottom: 10px;
        right: 12px;
      }
    }
  }
  .back {
    transform: rotateX(180deg) translateZ(10px);

    span {
      top: 26px;
      left: 26px;
    }
  }
  .right {
    transform: rotateY(90deg) translateZ(10px);

    span {
      &:nth-child(1) {
        top: 12px;
        left: 12px;
      }
      &:nth-child(2) {
        top: 12px;
        right: 12px;
      }
      &:nth-child(3) {
        top: 26px;
        left: 26px;
      }
      &:nth-child(4) {
        bottom: 12px;
        left: 12px;
      }
      &:nth-child(5) {
        bottom: 12px;
        right: 12px;
      }
    }
  }
  .left {
    transform: rotateY(-90deg) translateZ(10px);

    span {
      &:nth-child(1) {
        top: 12px;
        right: 12px;
      }
      &:nth-child(2) {
        bottom: 12px;
        left: 12px;
      }
    }
  }
  .top {
    transform: rotateX(90deg) translateZ(10px);
    height: 20px;
    span {
      &:nth-child(1) {
        top: 12px;
        right: 12px;
      }
      &:nth-child(2) {
        bottom: 12px;
        left: 12px;
      }
      &:nth-child(3) {
        bottom: 26px;
        left: 26px;
      }
    }
  }
  .bottom {
    transform: rotateX(-90deg) translateZ(192px);
    height: 20px;
    span {
      &:nth-child(1) {
        top: 12px;
        right: 12px;
      }
      &:nth-child(2) {
        top: 12px;
        left: 12px;
      }
      &:nth-child(3) {
        bottom: 12px;
        left: 12px;
      }
      &:nth-child(4) {
        bottom: 12px;
        right: 12px;
      }
    }
  }
}

.button {
  position: fixed;
  bottom: 20px;
  background: #f76939;
  padding: 20px 40px;
  border-radius: 4px;
  color: #fff;
  cursor: pointer;

  &:hover {
    background: #f76939 - 20;
  }
}

@keyframes opacity {
  0% {
    opacity: 1;
  }
  20% {
    opacity: 0.5;
  }
  40% {
    opacity: 1;
  }
  60% {
    opacity: 1;
  }
  80% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}

@keyframes rotate {
  0% {
    transform: rotateY(0deg) translateX(0px);
  }
  //  35% { transform: rotateX(-180deg) rotateY(-90deg) rotateZ(0deg) translateX(0); }
  //  45% { transform: rotateX(-180deg) rotateY(-90deg) rotateZ(0deg) translateX(0); }
  //  65% { transform: rotateX(0deg) rotateY(0deg) rotateZ(-360deg) translateX(0); }
  //  75% { transform: rotateX(0deg) rotateY(0deg) rotateZ(-360deg) translateX(0); }
  100% {
    transform: rotateY(18000deg) translateX(0px);
    transition-delay: 1s;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
<script>
export default {
  name: "Dice",
  props: {
    animate: { type: Object, default: () => ({}) }
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
      rotateDeg: 0
    };
  },
  methods: {
    beforeEnter: function() {
      console.log("beforenter");
    },
    enter: function() {
      console.log("enter");
    },
    swipeTigger(animate) {
      let dx = animate.x - animate.x1;
      let dy = animate.y - animate.y1;

      const radians = Math.atan2(dy, dx);
      var pi = Math.PI;
      this.rotateDeg = radians * (180 / pi);
      return this.rotateDeg;
    },
    showDice() {
      this.show = !this.show;
    }
  },
  watch: {
    animate(val) {
      this.swipeTigger(val);
    }
  },
  computed: {
    classObject() {
      return {
        transform:
          "rotateZ(" +
          (this.rotateDeg / 10) * Math.random() * 1 +
          "deg) rotateY(" +
          Math.ceil(Math.random() * 10) * 90 +
          "deg) translateX(" +
          Math.random() * 50 +
          "px) translateY(" +
          Math.random() * 50 +
          "px)",
        transition: `transform 0.3s`
      };
    }
  }
};
</script>
