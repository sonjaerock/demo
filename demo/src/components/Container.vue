<template>
  <div id="app">
    <div
      class="demo"
      v-for="option in options"
      :key="option.id">
      <demo :option="option"></demo>
    </div>
  </div>
</template>

<script>
  import Lottie from './lottie.vue';
  import Demo from './Demo.vue';
  import * as LoadingAnimation from '../assets/loading_animation.json';
  import * as InfiniteLoop from '../assets/infinite_loop.json';
  import * as BotAnimation from '../assets/bot_typing.json';
  import * as CheckAnimation from '../assets/check_animation.json';
  import * as GreenRadialsAnimation from '../assets/loading_green_radials.json';

  export default {
    name: 'Container',
    components: {
      'lottie': Lottie,
      'demo' : Demo
    },
    data() {
      return {
        options: [
          {
            animationData: LoadingAnimation,
            id: 1
          },
          {
            animationData: InfiniteLoop,
            id: 2
          },
          {
            animationData: BotAnimation,
            id: 3
          },
          {
            animationData: CheckAnimation,
            id: 4
          },
          {
            animationData: GreenRadialsAnimation,
            id: 5
          },
        ]
      }
    }
  }
</script>
<style scoped>
  .demo {
    width: 18%;
    margin-left: 1%;
    margin-right: 1%;
    float: left;
  }

  @media screen and (max-width: 1000px) {
    .demo { width: 31%; }
  }
</style>
