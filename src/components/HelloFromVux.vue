<template>
  <div>
    <div class="vux-demo">
      <!--<x-header style="background-color:#9acdeb;" :left-options="{showBack: false}">橙子之家</x-header>-->
      <div  class="container">
        <div class="backgroundImageFilter"></div>
        <h2 style="color: blanchedalmond">CXM ♥ CH</h2>
        <!--<h3 style="color: blanchedalmond">程旭敏 & 程慧</h3>-->
      </div>
      <marquee>
        <marquee-item v-for="i in tips" :key="i.msg" @click.native="onClick(i)" class="align-middle">{{i.msg}}</marquee-item>
      </marquee>
      <divider>距离一周年还有:</divider>
      <div>
        <clocker :time="timeWeFallInLove"></clocker>
      </div>
    </div>
    <div style="margin: 10px;overflow: hidden;" v-for="item in maskerList">
      <masker style="border-radius: 2px;">
        <div class="m-img" :style="{backgroundImage: 'url(' + item.img + ')'}"></div>
        <div slot="content" class="m-title">
          {{item.title}}
          <br/>
          <span class="m-time">{{item.time}}</span>
        </div>
      </masker>
    </div>

    <card>
      <!--<img slot="header" src="http://placeholder.qiniudn.com/640x300" style="width:100%;display:block;">-->
      <div slot="content" class="card-padding">
        <p style="color:#999;font-size:12px;">虽然我不怎么懂浪漫、脾气也很不好，反正缺点真的挺多的</p>
        <p style="font-size:14px;line-height:1.2;">但这辈子，我想一直和你在一起，往后余生，我会为你而改变，慢慢学着浪漫起来，慢慢改改自己的脾气，我也相信你会跟我一起努力，咱们以后一定要变得很有钱hhh，一定会一直幸福下去的。宝贝20岁生日快乐~</p>
        <p style="color:#999;font-size:12px;margin-left: 57%">---To: 程慧小宝贝</p>
      </div>
      <div v-transfer-dom>
        <previewer :list="list" ref="previewer" :options="options" @on-index-change="logIndexChange"></previewer>
      </div>
    </card>
    <!--<div style="margin-left: 10%;margin-right: 10%">-->
      <!--<img class="previewer-demo-img" v-for="(item, index) in list" :src="item.src" width="100" @click="show(index)">-->
      <!--<div v-transfer-dom>-->
        <!--<previewer :list="list" ref="previewer" :options="options" @on-index-change="logIndexChange"></previewer>-->
      <!--</div>-->
    <!--</div>-->
  </div>
</template>

<script>
import { Group, Cell,XHeader,Clocker,Marquee, MarqueeItem, Divider,Previewer,TransferDom,Swiper,Masker,Card} from 'vux'

export default {
  directives: {
    TransferDom
  },
  components: {
    Group,
    Cell,
    XHeader,
    Clocker,
    Marquee,
    MarqueeItem,
    Divider,
    Previewer,
    Swiper,
    Masker,
    Card,
  },
  mounted () {
    setTimeout(() => {
      this.asyncCount = 5
    }, 1000)
  },
  methods: {
    onClick (i) {
      console.log(i)
    },
    logIndexChange (arg) {
      console.log(arg)
    },
    show (index) {
      this.$refs.previewer.show(index)
    },
    swiperOnIndexChange (index) {
      this.swiper_index = index
    },
  },
  data () {
    return {
      // note: changing this line won't causes changes
      // with hot-reload because the reloaded component
      // preserves its current state and we are modifying
      // its initial state.
      msg: 'Hello World!',
      timeWeFallInLove:'2020-06-03',
      asyncCount: 0,
      //浏览图片
      list: [{
        msrc: 'https://i.postimg.cc/VJq9bb8h/20191028154007.jpg',
        src: 'https://i.postimg.cc/BnymkxwJ/20191028154007.jpg',
        // w: 800,
        // h: 400,
      },
        {
          msrc: 'https://i.postimg.cc/5HfB5N92/25dbd3e6f50e44fb1946e82db560824.jpg',
          src: 'https://i.postimg.cc/W4k5vhQg/25dbd3e6f50e44fb1946e82db560824.jpg',
        }, {
          msrc: 'http://ww1.sinaimg.cn/thumbnail/663d3650gy1fplwwcynw2j20p00b4js9.jpg',
          src: 'http://ww1.sinaimg.cn/large/663d3650gy1fplwwcynw2j20p00b4js9.jpg',
        }],
      options: {
        getThumbBoundsFn (index) {
          // find thumbnail element
          let thumbnail = document.querySelectorAll('.previewer-demo-img')[index]
          // get window scroll Y
          let pageYScroll = window.pageYOffset || document.documentElement.scrollTop
          // optionally get horizontal scroll
          // get position of element relative to viewport
          let rect = thumbnail.getBoundingClientRect()
          // w = width
          return {x: rect.left, y: rect.top + pageYScroll, w: rect.width}
          // Good guide on how to get element coordinates:
          // http://javascript.info/tutorial/coordinates
        }
      },
      //轮播列表
      tips:[
        {msg:'宝贝喜欢燕麦黄桃味的安慕希'},
        {msg:'宝贝不喜欢香菜'},
        {msg:'宝贝吃鱼腥草会胃痛'},
        {msg:'宝贝喜欢灰色的垂耳兔'},
        {msg:'宝贝喜欢柴犬'},
        {msg:'宝贝肝肾不好，得注意她的饮食'},
        {msg:'宝贝不喜欢榴莲'},
        {msg:'宝贝喜欢抹茶'},
        {msg:'宝贝看电影喜欢坐左边'},
      ],
      //swiper
      swiper_index: 0,
      //masker
      maskerList: [{
        title: '那天你来我家，我们时隔十年再次相遇了',
        img: 'https://i.postimg.cc/VJq9bb8h/20191028154007.jpg',
        time:'2019-05-25'
      }, {
        title: '我们聊得很投缘，那个周一，我们在一起了',
        img: 'https://i.postimg.cc/W4k5vhQg/25dbd3e6f50e44fb1946e82db560824.jpg',
        time:'2019-06-03'
      }, {
        title: '端午节，你回杭州，那三天真的很开心，但你的牙，真的很菜哦，hhh',
        img: 'https://i.postimg.cc/Z5FFjDDN/f37931a26309b94c4dd14fdd35e2aff.jpg',
        time:'2019-06-07'
      }, {
        title: '那是我第一次去你的学校陪你，你在车站送我回去的时候，我真的很不舍得你',
        img: 'https://i.postimg.cc/VJq9bb8h/20191028154007.jpg',
        time:'2019-06-16'
      },{
        title: '你终于放暑假啦！那是我们第一次一起做陶瓷',
        img: 'https://i.postimg.cc/VJq9bb8h/20191028154007.jpg',
        time:'2019-07-06'
      }, {
        title: '这是我们第一次去旅行哦，南京之旅真的很不错（忽略哥老关）',
        img: 'https://i.postimg.cc/W4k5vhQg/25dbd3e6f50e44fb1946e82db560824.jpg',
        time:'2019-07-12'
      }, {
        title: '端午节，你回杭州，那三天真的很开心，但你的牙，真的很菜哦，hhh',
        img: 'https://i.postimg.cc/VJq9bb8h/20191028154007.jpg',
        time:'2019-06-07'
      }, {
        title: '那是我第一次去你的学校陪你，你在车站送我回去的时候，我真的很不舍得你',
        img: 'https://i.postimg.cc/VJq9bb8h/20191028154007.jpg',
        time:'2019-06-16'
      }
      ]
    }
  }
}
</script>

<style>
.vux-demo {
  text-align: center;
}
.backgroundImageFilter,
.container {
  width: 360px;
  height: 300px;
  font-size: 30px;
  text-align: center;
  line-height: 300px;
}
.container {
  margin: 0 auto;
  position: relative;
}
.backgroundImageFilter {
  position: absolute;
  background-image: url('https://i.postimg.cc/Z5FFjDDN/f37931a26309b94c4dd14fdd35e2aff.jpg');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  background-position: center;
  z-index: -1;
  transition: filter 1s;
  filter: blur(5px);
}
/*.container:hover  .backgroundImageFilter {*/
  /*filter: blur(20px);*/
/*}*/
.previewer-demo-img{
  border: 5px solid #c5dce9;
  width: 80px;
  height: 80px;
  border-radius: 5px;
  margin-left: 5px;
}
/*masker*/
.m-img {
  padding-bottom: 33%;
  display: block;
  position: relative;
  max-width: 100%;
  background-size: cover;
  background-position: center center;
  cursor: pointer;
  border-radius: 2px;
}

.m-title {
  color: #fff;
  text-align: center;
  text-shadow: 0 0 2px rgba(0, 0, 0, .5);
  font-weight: 500;
  font-size: 16px;
  position: absolute;
  left: 0;
  right: 0;
  width: 100%;
  text-align: center;
  top: 50%;
  transform: translateY(-50%);
}

.m-time {
  font-size: 12px;
  padding-top: 4px;
  border-top: 1px solid #f0f0f0;
  display: inline-block;
  margin-top: 5px;
}
.card-padding {
  padding: 35px;
}
</style>
