<template>
  <div class="wrapper">
    <swiper :options="swiperOption" ref="mySwiper" v-if="showSwiper">
      <swiper-slide v-for="item of swiperList" :key="item.id">
        <img class="sweiper-img" :src="item.imgUrl">
      </swiper-slide>
      <div class="swiper-pagination"  slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  data () {
    return {
      swiperOption: {
        pagination: {
          el: '.swiper-pagination',
          type: 'bullets'
        },
        loop: true,
        autoplay: {
          delay: 3000
        }
      }
    }
  },
  props: {
    swiperList: {
      type: Array,
      default () {
        return []
      }
    }
  },
  computed: {
    showSwiper () {
      return this.swiperList.length
    }
  }
}
</script>

<style lang="stylus" scoped>
  .wrapper >>>.swiper-pagination-bullet-active
    background: #fff !important
  .wrapper
    width: 100%
    height: 0
    overflow: hidden
    padding-bottom: 30.25%
    .sweiper-img
      width: 100%
</style>
