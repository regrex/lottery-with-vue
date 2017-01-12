<template>
  <div>
    <ul class="m-list">
      <li class="m-item" v-bind:class="'m-item-' + (index % 5)" v-for="(item, index) in list" v-if="index < 5">
        <img class="m-img" :src="item.img" alt="头像">
        <p class="m-title">
          {{item.title}}
        </p>
      </li>
    </ul>
  </div>
</template>

<script>
import { Masker, XHeader, XButton } from 'vux'

export default {
  components: {
    XButton,
    Masker
  },
  data () {
    return {
      list: [{
        title: '姓名三',
        img: 'https://cdn.xiaotaojiang.com/uploads/82/1572ec37969ee263735262dc017975/_.jpg'
      }, {
        title: '姓名1',
        img: 'https://cdn.xiaotaojiang.com/uploads/59/b22e0e62363a4a652f28630b3233b9/_.jpg'
      }, {
        title: '姓名二',
        img: 'https://cdn.xiaotaojiang.com/uploads/59/b22e0e62363a4a652f28630b3233b9/_.jpg'
      }, {
        title: '姓名1',
        img: 'https://cdn.xiaotaojiang.com/uploads/59/b22e0e62363a4a652f28630b3233b9/_.jpg'
      }, {
        title: '姓名二',
        img: 'https://cdn.xiaotaojiang.com/uploads/56/4b3601364b86fdfd234ef11d8712ad/_.jpg'
      }, {
        title: '姓名1',
        img: 'https://cdn.xiaotaojiang.com/uploads/59/b22e0e62363a4a652f28630b3233b9/_.jpg'
      }, {
        title: '姓名二',
        img: 'https://cdn.xiaotaojiang.com/uploads/56/4b3601364b86fdfd234ef11d8712ad/_.jpg'
      }, {
        title: '姓名1',
        img: 'https://cdn.xiaotaojiang.com/uploads/59/b22e0e62363a4a652f28630b3233b9/_.jpg'
      }, {
        title: '姓名二',
        img: 'https://cdn.xiaotaojiang.com/uploads/56/4b3601364b86fdfd234ef11d8712ad/_.jpg'
      }]
    }
  }
}
</script>

<style lang="less">
.vux-header {
  background-color: #4A90E2;
}
.m-img {
  width: 100%;
}
.m-title {
  position: absolute;
  bottom: 0;
  color: #fff;
  width: 100%;
  padding: 4px;
  text-align: center;
}

.m-time {
  font-size: 12px;
  padding-top: 4px;
  border-top: 1px solid #f0f0f0;
  display: inline-block;
  margin-top: 5px;
}
.m-list {
  position: relative;
  width: 580px;
  height: 224px;
  margin: 0 auto;
}
.m-item {
  width: 266px;
  height: 216px;
  border: 2px solid #fff;
  overflow: hidden;
  position: absolute;
  cursor: pointer;
}
.m-item-0 {
    top: 70px;
    left: 45px;
    height: 116px;
    width: 140px;
    z-index: 100;
    border-color: #e8ad0e;
    .m-title {
        background-color: #e8ad0e;
    }
    .m-img {
        border-color: #e8ad0e;
    }
    .m-time {
        span {
            background: #e8ad0e;
        }
        i {
            border-color: #b58608;
        }
    }
}        
.m-item-1 {
    top: 45px;
    left: 95px;
    height: 160px;
    width: 196px;
    z-index: 200;
    border-color: #2998ff;
    .m-title {
        background-color: #2998ff;
    }
    .m-img {
        border-color: #2998ff;
    }
    .m-time {
        span {
            background: #ff2970;
        }
        i {
            border-color: #e7165b;
        }
    }
}        
.m-item-2 {
    top: 20px;
    left: 160px;
    z-index: 300;
    border-color: #a035f7;
    .m-title {
        background-color: #a035f7;
    }
    .m-img {
        border-color: #a035f7;
    }
    .m-time {
        span {
            background: #fa4848;
        }
        i {
            border-color: #d93f3f;
        }
    }
}
.m-item-3 {
    top: 45px;
    right: 95px;
    height: 160px;
    width: 196px;
    z-index: 200;
    border-color: #05ae8e;
    .m-title {
        background-color: #05ae8e;
    }
    .m-img {
        border-color: #05ae8e;
    }
    .m-time {
        span {
            background: #ff7800;
        }
        i {
            border-color: #ee7408;
        }
    }
}
.m-item-4 {
    top: 70px;
    right: 45px;
    height: 116px;
    width: 140px;
    z-index: 100;
    border-color: #df3444;
    .m-title {
        background-color: #df3444;
    }
    .m-img {
        border-color: #df3444;
    }
    .m-time {
        span {
            background: #fb4c92;
        }
        i {
            border-color: #e9387f;
        }
    }
}
</style>