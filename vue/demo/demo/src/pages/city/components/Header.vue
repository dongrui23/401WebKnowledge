<template>
  <div class='header'>
    城市选择
    <router-link to='./'>
      <span class="iconfont header-back">&#xe624;</span>
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'CityHeader'
}
</script>

<style lang='stylus' scoped>
  .header
    position: relative
    overflow: hidden
    height:.86rem
    line-height:.86rem
    text-align :center
    color:#fff
    background:#00bcd4
    font-size :.32rem
    .header-back
      top:0
      left:0
      position :absolute
      width:.64rem
      text-align :center
      font-size :.4rem
      color:#fff
</style>
