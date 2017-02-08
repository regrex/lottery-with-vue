<template>
  <div class="lottery-wrap">
    <h2 class="lottery-theme">欢度春节，中奖回家过年啰！</h2>
    <div class="lottery-operate">
      <button class="lottery-btn" @click="lottery">{{ (lotterying ? '停止' : '开始') + '第' + lotteryNum + '轮抽奖'}}</button>
      <input class="lucky-number" type="number" min="1" v-bind:max="list.length" v-model.number="luckyNum" @change="changeLuckyNum" />
    </div>
    <div class="lottery-list">
      <transition-group
        name="lottery"
        enter-active-class="animated fadeIn"
        leave-active-class="animated fadeOut"
        tag="div"
        >
        <div class="lottery-item list-complete-item" v-for="(item, index) in randomList" v-bind:key="index">
          <div class="lottery-item-inner">
            <a href="javascript:void(0)" @click="zoomIn({luckImg: item.img, luckyTitle: item.title})">
              <img class="lottery-img" v:show="item.img" :src="item.img" alt="头像">
              <p class="lottery-title">
                {{item.title}}
              </p>
            </a>
          </div>
        </div>
      </transition-group>
    </div>
    <div class="result-list">
      <transition-group name="list-complete" tag="div">
        <div class="lottery-item lucky-item list-complete-item" v-for="(luckyItem, lIndex) in luckyList" v-bind:key="lIndex">
          <span class="lucky-rank">{{luckyItem.luckyRank}}</span>
          <div class="lottery-item-inner">
            <a href="javascript:void(0)" @click="zoomIn({luckImg: luckyItem.luckyMan.img, luckyTitle: luckyItem.luckyMan.title})">
              <img class="lottery-img" :src="luckyItem.luckyMan.img" alt="头像">
            </a>
            <p class="lottery-title">
              {{luckyItem.luckyMan.title}}
            </p>
          </div>
        </div>
      </transition-group>
    </div>
    <transition name="zoom" enter-active-class="animated fadeIn" leave-active-class="animated fadeOut">
      <div class="zoom-wrap" v-if="zoomItem.luckImg">
        <div @click="zoomOut" class="zoom-masker"></div>
        <div class="zoom-item">
          <div class="zoom-item-inner">
            <span class="zoom-title">{{zoomItem.slogan}}</span>
            <img class="lottery-img" :src="zoomItem.luckImg" alt="头像">
            <p class="lottery-title">
              {{zoomItem.luckyTitle}}
            </p>
          </div>
        </div>
      </div>
    </transition>
    <button v-if="luckyList.length !== 0" class="clear-lucky-btn" @click="clearCurLuckyList">清除当前中奖记录</button>
    <!-- <button v-if="luckyList.length !== 0" class="clear-lucky-btn" @click="clearLuckyList">清除历史中奖记录</button> -->
  </div>
</template>

<script>

let lotteryTimer = 0;
export default {
  components: {
  },
  methods: {
    randomIndex: function (randomList) {
      return Math.floor(Math.random() * randomList.length);
    },
    changeLuckyNum: function (e) {
      let luckyNum = e.target.value;
      if (luckyNum < 0) {
        this.luckyNum = 1;
      }
      if (luckyNum > (this.list.length - luckyNum)) {
        this.luckyNum = this.list.length - luckyNum;
      }
      return;
    },
    removeToLuck: function () {
      let self = this;
      let lucky = self.list.splice(self.randomIndex(self.list), 1);
      self.luckyList.unshift({
        luckyRank: self.lotteryNum,
        luckyMan: lucky[0]
      });
    },
    lottery: function () {
      let self = this;

      // console.log(self.list.length - self.luckyNum);
      // if (self.luckyNum >= (self.list.length - self.luckyNum)) {
      //   alert('剩余未中奖人数小于发奖数量！');
      //   return;
      // }

      if (!self.lotterying) {
        lotteryTimer = setInterval(() => {
          self.list = _.shuffle(self.list);
          for(let i = 0; i < self.randomList.length; i++) {
            self.randomList[i] = self.list[i];
          }
          self.randomList = _.shuffle(self.randomList);
        }, 100);
      } else {
        clearInterval(lotteryTimer);
        for (let i = 0; i < self.luckyNum; i++) {
          self.removeToLuck();
        }
        window.localStorage.setItem('luckyList', JSON.stringify(self.luckyList));
        self.lotteryNum++;
      }

      self.lotterying = !self.lotterying;
    },
    zoomIn: function(item, e) {
      item.slogan = this.sloganList[this.randomIndex(this.sloganList)];
      this.zoomItem = item;
    },
    zoomOut: function() {
      this.zoomItem = {};
    },
    clearCurLuckyList: function() {
      this.lotteryNum = 1;
      this.luckyList = [];
    },
    clearLuckyList: function() {
      window.localStorage.setItem('luckyList', JSON.stringify([]));
      this.lotteryNum = 1;
      this.luckyList = [];
    }
  },
  data () {
    return {
      sloganList: [
        '我有我风格',
        '怎么可以这么美',
        '不要迷恋我，我只是传说',
        '有没有闪瞎你？',
        '我美，我媚~',
        '嘿嘿╮(╯_╰)╭',
        '据说长得像我的人更容易中奖',
        '再看我，再看我就把你带走',
        '我就是冒个泡而已',
        '怎么我又被围观了',
        '我只想做一个安静的美男子',
        '谁在侵犯我的肖像权！',
        '他们都在看我，我好害羞',
        '为啥要点开我的照片，不开森',
        'Hello World',
        '看到我的人更容易集齐五福',
        '天啊，这是我嘛！'
      ],
      list: [
        {title: '1', img: '../../static/1.jpg'},
        {title: '2', img: '../../static/2.jpg'},
        {title: '3', img: '../../static/3.jpg'},
        {title: '4', img: '../../static/4.jpg'},
        {title: '5', img: '../../static/5.jpg'},
        {title: '6', img: '../../static/6.jpg'},
        {title: '7', img: '../../static/7.jpg'},
        {title: '8', img: '../../static/8.jpg'},
        {title: '9', img: '../../static/9.jpg'},
        {title: '10', img: '../../static/10.jpg'},
        {title: '11', img: '../../static/11.jpg'},
        {title: '12', img: '../../static/12.jpg'},
        {title: '13', img: '../../static/13.jpg'},
        {title: '14', img: '../../static/14.jpg'},
        {title: '15', img: '../../static/15.jpg'},
        {title: '16', img: '../../static/16.jpg'},
        {title: '17', img: '../../static/17.jpg'},
        {title: '18', img: '../../static/18.jpg'},
        {title: '19', img: '../../static/19.jpg'},
        {title: '20', img: '../../static/20.jpg'},
        {title: '21', img: '../../static/21.jpg'},
        {title: '22', img: '../../static/22.jpg'},
        {title: '23', img: '../../static/23.jpg'},
        {title: '24', img: '../../static/24.jpg'},
        {title: '25', img: '../../static/25.jpg'},
        {title: '26', img: '../../static/26.jpg'},
        {title: '27', img: '../../static/27.jpg'},
        {title: '28', img: '../../static/28.jpg'},
        {title: '29', img: '../../static/29.jpg'},
        {title: '30', img: '../../static/30.jpg'},
        {title: '31', img: '../../static/31.jpg'},
        {title: '32', img: '../../static/32.jpg'},
        {title: '33', img: '../../static/33.jpg'},
        {title: '34', img: '../../static/34.jpg'},
        {title: '35', img: '../../static/35.jpg'},
        {title: '36', img: '../../static/36.jpg'}
      ],
      randomList: [
        {title: '9', img: '../../static/9.jpg'},
        {title: '10', img: '../../static/10.jpg'},
        {title: '11', img: '../../static/11.jpg'},
        {title: '12', img: '../../static/12.jpg'},
        {title: '13', img: '../../static/13.jpg'},
        {title: '14', img: '../../static/14.jpg'},
        {title: '15', img: '../../static/15.jpg'},
        {title: '16', img: '../../static/16.jpg'},
        {title: '17', img: '../../static/17.jpg'},
        {title: '18', img: '../../static/18.jpg'},
        {title: '19', img: '../../static/19.jpg'},
        {title: '20', img: '../../static/20.jpg'},
        {title: '21', img: '../../static/21.jpg'},
        {title: '22', img: '../../static/22.jpg'},
        {title: '23', img: '../../static/23.jpg'},
        {title: '24', img: '../../static/24.jpg'},
        {title: '25', img: '../../static/25.jpg'},
        {title: '26', img: '../../static/26.jpg'},
        {title: '27', img: '../../static/27.jpg'},
        {title: '28', img: '../../static/28.jpg'},
        {title: '29', img: '../../static/29.jpg'},
        {title: '30', img: '../../static/30.jpg'},
        {title: '31', img: '../../static/31.jpg'},
        {title: '32', img: '../../static/32.jpg'}
      ],
      luckyList: JSON.parse(window.localStorage.getItem('luckyList')) || [],
      resultList: [],
      lotterying: false,
      luckyNum: 1,
      lotteryNum: 1,
      zoomItem: {}
    }
  }
}
</script>

<style>
.lottery-wrap {
  text-align: center;
}
.lottery-theme {
  color: #FFEB3B;
  text-align: center;
  font-family: sans-serif;
  font-size: 40px;
  text-shadow: #FFC107 0px 0px 10px;
}
.lottery-operate {
  text-align: center;
}
.lottery-btn {
  width: 150px;
  height: 150px;
  background: rgb(76, 175, 80) url(../assets/btn-bg.png) no-repeat center center;
  border: 0;
  background-size: contain;
  color: #FFEB3B;
  border-radius: 50%;
  font-size: 20px;
  padding: 30px;
  outline: 0;
}
.lottery-list {
  width: 880px;
  height: 220px;
  margin: 20px auto;
  overflow: hidden;
}

.list-complete-item {
  transition: all 1s ease-in-out;
  display: inline-block;
  margin-right: 10px;
}

.list-complete-enter, .list-complete-leave-active {
  opacity: 0;
  transform: translateY(20px);
}
.list-complete-leave-active {
  position: absolute;
}

.lottery-item {
  position: relative;
  width: 100px;
  height: 100px;
  margin-bottom: 10px;
}

.lottery-item-inner {
  display: block;
  width: 100%;
  height: 100%;
  overflow: hidden;
  position: relative;
}
.lottery-img {
  width: 100%;
  height: 100%;
}
.lottery-title {
  position: absolute;
  bottom: 0;
  left: 0;
  padding: 5px 0;
  color: #fff;
  width: 100%;
  text-align: center;
  background-color: rgba(0, 0, 0, 0.31);
}
.lottery-operate {
  width: 60%;
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.lucky-number {
  width: 60px;
  padding: 0 10px;
  font-size: 20px;
  border: 0;
  background: rgba(255, 255, 255, 0.61);
  height: 40px;
  border-radius: 4px;
  color: #FFEB3B;
}
.lottery-item.lucky-item {
  box-shadow: 0 0 6px 2px #FFEB3B;
  border-radius: 50%;
}
.lucky-item .lottery-item-inner {
  border-radius: 50%;
}
.lucky-item::before {
  content: '';
  position: absolute;
  left: -32px;
  top: -34px;
  display: block;
  width: 71px;
  height: 64px;
  background: url(../assets/crown.png) no-repeat 0 0;
  background-size: contain;
}
.lucky-rank {
  position: absolute;
  left: 8px;
  top: -12px;
  color: #dc0a17;
  font-size: 20px;
  transform: rotate(-45deg);
  font-family: fantasy;
  font-weight: bold;
}

.animated {
  animation-duration: 0.5s;
  animation-fill-mode: both;
}

.animated.infinite {
  animation-iteration-count: infinite;
}

.result-list {
  width: 880px;
  margin: 40px auto 0 auto;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

.fadeIn {
  -webkit-animation-name: fadeIn;
  animation-name: fadeIn;
}

@keyframes fadeOut {
  from {
    opacity: 1;
  }

  to {
    opacity: 0;
  }
}

.fadeOut {
  -webkit-animation-name: fadeOut;
  animation-name: fadeOut;
}

.zoom-masker {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.61);
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
}

.zoom-item {
  position: fixed;
  width: 400px;
  height: 400px;
  left: 50%;
  top: 50%;
  margin-left: -200px;
  margin-top: -200px;
}
.zoom-item-inner {
  height: 400px;
  overflow: hidden;
  position: relative;
  text-align: center;
}
.zoom-title {
  color: yellow;
  font-size: 28px;
  line-height: 1.25;
}

.clear-lucky-btn {
  border: 1px solid #FF9800;
  background: #FFC107;
  font-size: 16px;
  padding: 10px;
  border-radius: 4px;
  color: #dc0a17;
  margin: 30px auto;
}
</style>