<template>
  <div id="app">

    <lottie
      :id="option.id"
      :options="option"
      v-on:animCreated="handleAnimation"/>

    <div class="option-box">
      <span>속도 조절 Speed: x{{animationSpeed}}</span>
      <input
        type="range"
        value="1"
        min="0"
        max="3"
        step="0.5"
        v-on:change="onSpeedChange"
        v-model="animationSpeed">
    </div>


    <div class="option-box">
      <span>기본 동작</span>
      <button v-on:click="stop(animationSpeed)">stop</button>
      <button v-on:click="pause(animationSpeed)">pause</button>
      <button v-on:click="play(animationSpeed)">play</button>
    </div>


    <div class="option-box">
      <span>특정시점에 멈추기</span>
      <input
        type="range"
        value="1"
        min="0"
        max="50"
        step="10"
        v-on:change="goToAndStop(stopTime, true)"
        v-model="stopTime">
    </div>


    <div class="option-box">
      <span>특정시점에 시작하기</span>
      <input
        type="range"
        value="1"
        min="0"
        max="50"
        step="10"
        v-on:change="goToAndPlay(playTime, true)"
        v-model="playTime">
    </div>

    <div class="option-box">
      <span>방향바꾸기</span>
      <button @click="setDirection()">방향전환</button>
    </div>

    <div class="option-box">
      <div style="text-align: left;">동작 구간 설정하기</div>

      <div>
        <div style="text-align: left;">
          Start Frame :
          <input
            type="range"
            value="1"
            min="0"
            max="50"
            step="10"
            v-on:change="playSegments(segments, true)"
            v-model="segments[0]">
        </div>
        <div style="text-align: left;">
          End Frame :
          <input
            type="range"
            value="1"
            min="0"
            max="50"
            step="10"
            v-on:change="playSegments(segments, true)"
            v-model="segments[1]">
        </div>
      </div>
    </div>


    <!--<div class="option-box">-->
      <!--<span>방향바꾸기</span>-->
      <!--<button @click="setSubframe()">방향전환</button>-->
    <!--</div>-->


    <div class="option-box">
      <div>파괴</div>
      <button @click="destroy()">파괴한다</button>
    </div>
  </div>

</template>

<script>
  import Lottie from './lottie.vue';

  export default {
    name: 'Demo',
    props: {
      option: Object,
      default: function () {
        return null
      }
    },
    components: {
      'lottie': Lottie
    },
    data() {
      return {
        animationSpeed: 1,
        stopTime: 0,
        playTime: 0,
        directionFlag: 1,
        segments: [0, 0],
        subFrameFlag: true
      }
    },
    methods: {
      handleAnimation: function (anim) {
        this.anim = anim;
      },

      stop: function () {
        this.anim.stop();
      },

      play: function () {
        this.anim.play();
      },

      pause: function () {
        this.anim.pause();
      },

      onSpeedChange: function () {
        this.anim.setSpeed(this.animationSpeed);
      },

      goToAndStop: function (value, isFrame) {
        this.anim.goToAndStop(value * 1, isFrame);
      },

      goToAndPlay: function (value, isFrame) {
        this.anim.goToAndPlay(value * 1, isFrame);
      },

      setDirection: function () {
        this.directionFlag = this.directionFlag * -1;
        this.anim.setDirection(this.directionFlag);
      },

      playSegments: function (segments, forceFlag) {
        this.anim.playSegments(segments, forceFlag)
      },

      // setSubframe: function() {
      //   this.anim.setSubframe(!this.subFrameFlag);
      // }

      destroy: function () {
        this.anim.destroy();
      }

    }
  }
</script>
<style>
  * {
    font-size: 13px;
  }

  p {
    float: left;
  }

  .option-box {
    float: left;
    margin-top: 20px;
    margin-bottom: 20px;
    width: 100%;
    text-align: left;
  }
</style>
