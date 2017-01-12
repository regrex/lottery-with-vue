<template>
  <div>
    <x-header :right-options="{showMore: true}" :left-options="{showBack: false}" @on-click-more="showMenus = true">抽奖走起来</x-header>
    <actionsheet :menus="menus" v-model="showMenus" show-cancel></actionsheet>
  </div>
</template>

<script>
import { XHeader, Actionsheet, Group, Cell, XButton } from 'vux'

export default {
  components: {
    Group,
    Cell,
    XButton,
    XHeader,
    Actionsheet
  },
  data () {
    return {
      menus: {
        menu1: '更改人数',
        menu2: '清空数据'
      },
      showMenus: false
    }
  }
}
</script>

<style>
.vux-demo {
  text-align: center;
}
.logo {
  width: 100px;
  height: 100px
}
</style>