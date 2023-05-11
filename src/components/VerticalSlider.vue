<template>
    <swiper class="swiper" :options="swiperOption" noSwiping id="swiperContainer" ref="swiper">
        <swiper-slide v-for="item in items" :key="item.title" class="swiper-no-swiping">{{ item.title }}</swiper-slide>
        <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
</template>
  
<script>
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
import 'swiper/css/swiper.css'

export default {
    name: 'swiper-example-vertical',
    title: 'Vertical slider',
    props: ['items'],
    components: {
        Swiper,
        SwiperSlide
    },
    data() {
        return {
            swiperOption: {
                direction: 'vertical',
                pagination: {
                    el: '.swiper-pagination',
                    clickable: true
                },
                freeMode: true,
                onReachBeginning: this.slideNext,
                noSwiping: true
            },
            swiper: null,
            reachedStart: false,
        }
    },
    methods: {
        slideTo(slideToNumber) {
            this.$refs.swiper.$swiper.slideTo(slideToNumber);
        }
    },
}
</script>
<style>
.swiper {
    height: 300px;
    width: 80%;
    margin: 0 auto;
    border: 1px solid lightblue;
}

.swiper-slide {
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    font-weight: bold;
    font-size: 16px;
    background-color: white;
}
</style>