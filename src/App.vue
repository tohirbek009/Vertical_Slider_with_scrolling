<template>
  <div id="app">
    <div class="wrapper">
      <img alt="Vue logo" src="./assets/logo.png">
      <TopComponent></TopComponent>
      <VerticalSlider :items="swiperItems" ref="verticalSlider"/>
      <BottomComponent></BottomComponent>
    </div>
  </div>
</template>

<script>
import TopComponent from './components/TopComponent.vue';
import VerticalSlider from './components/VerticalSlider.vue';
import BottomComponent from './components/BottomComponent.vue';

export default {
  name: 'App',
  components: {
    TopComponent,
    VerticalSlider,
    BottomComponent
  },
  data() {
    return {
      swiperItems: [
        { title: "Slide 1" }, { title: "Slide 2" }, { title: "Slide 3" }, { title: "Slide 4" }, { title: "Slide 5" },
        { title: "Slide 6" }, { title: "Slide 7" }, { title: "Slide 8" }, { title: "Slide 9" }, { title: "Slide 10" },
      ],
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll() {
      const appElement = document.getElementById('app');
      const appElementRect = appElement.getBoundingClientRect();

      const swiperElement = document.getElementById('swiperContainer');
      const swiperTop = swiperElement.offsetTop;
      const allSwiperElementsHeight = swiperElement.offsetHeight * this.swiperItems.length;

      const limit = swiperTop - window.innerHeight * 0.25;

      const wrapperElement = document.getElementsByClassName('wrapper')[0];

      if ((-1)*appElementRect.top < limit) {
        wrapperElement.style.transform = `translate3d(0px, ${appElementRect.top}px, 0px)`;
      } 
      else {
        const slideToNumber = Math.floor(((-1)*appElementRect.top - limit) / swiperElement.offsetHeight);
        this.$refs.verticalSlider.slideTo(slideToNumber);
      }

      if ((-1)*appElementRect.top > allSwiperElementsHeight + limit) {
        wrapperElement.style.transform = `translate3d(0px, ${appElementRect.top + allSwiperElementsHeight}px, 0px)`;
      }

    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  min-height: 5000px;
  position: relative;
}

#app .wrapper {
  position: fixed;
  top: 0;
  left: 0;
}

body {
  margin: 0;
  padding: 0;
}
</style>
