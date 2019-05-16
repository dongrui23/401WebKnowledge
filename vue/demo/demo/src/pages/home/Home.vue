<template>
  <div>
    <home-header></home-header>
    <home-icons></home-icons>
    <home-recommend></home-recommend>
    <home-swiper></home-swiper>
    <home-weekend></home-weekend>
  </div>
</template>

<script>
import HomeHeader from './components/Header'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeSwiper from './components/Swiper'
import HomeWeekend from './components/Weekend'
export default {
  name: 'Home',
  components: {
    HomeHeader,
    HomeIcons,
    HomeRecommend,
    HomeSwiper,
    HomeWeekend
  }
}
</script>

<style>

</style>
