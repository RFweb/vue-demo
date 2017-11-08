<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{ msg1 }}</h2>
    
    <div v-html="message"></div>

    <label for="r1">修改颜色</label>
    <input type="checkbox" v-model="class1" id="r1">
    <br>
    <div v-bind:class="{'class1': class1}">
      directiva v-bind:class
    </div>

    {{5+5}}<br>
    {{ ok ? 'YES' : 'NO' }}<br>
    {{ message.split('').reverse().join('') }}
    <div v-bind:id="'list-' + id">今天
      <span v-if="rain === 0">晴天</span>
      <span v-else-if="rain === 1" >下雨了</span>
    </div>
    
    <pre><a v-bind:href="url">百度</a></pre>
    <!-- <pre><a :href="url">百度</a></pre> 缩写 -->
    
    <input v-model="inputTxt">
    <p>{{ inputTxt }}</p>
    <p>{{ num }}</p>
    <button v-on:click="numReduce">-</button>
    <!-- <button @click="numReduce">-</button> 缩写 -->
    <button v-on:click="numAdd">+</button>
    
    <br/>{{ author | capitalize }}<br/>
    <span v-show="ok">oo我出来了，因为OK===true</span>
    <br>
    <div id="run-box">
      <ul class="box">
        <li class="pic" :data-id="index" v-for="(value, index) in pics">
          <img :class="'img_' + index"  :src="value.url" alt="">
        </li>
      </ul>
    </div>
    <!-- <div class="pic">
      <img class="img-size" src="../assets/5.png" alt="">
    </div> -->

    <ul>
      <li v-for="value in object">
        {{ value }}
      </li>
    </ul>

  </div>
</template>

<script>
  import pic_1 from '../assets/1.jpg'
  import pic_2 from '../assets/2.png'
  import pic_3 from '../assets/3.jpg'
  import pic_4 from '../assets/4.png'
  import pic_5 from '../assets/6.png'
  import pic_6 from '../assets/7.png'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Hello World!',
      msg1: '你好！vue！',
      author: 'wly',
      message: '<span>文烈焰</span>',
      class1: false,
      id: 1,
      ok: true,
      rain: 1,
      url: 'http://www.baidu.com',
      inputTxt: 'Hello!你好！',
      num: 0,
      pics: [
        // { url: '../assets/1.jpg' },
        // { url: '../assets/2.png' },
        // { url: '../assets/3.jpg' },
        // { url: '../assets/4.png' },
        // { url: '../assets/6.png' },
        // { url: '../assets/7.png' }
        { url: pic_1 },
        { url: pic_2 },
        { url: pic_3 },
        { url: pic_4 },
        { url: pic_5 },
        { url: pic_6 }
      ],
      object: {
        name: '菜鸟教程',
        url: 'http://www.runoob.com',
        slogan: '学的不仅是技术，更是梦想！'
      }
    }
  },
  methods: {
    numAdd: function () {
      this.num += 1
    },
    numReduce: function () {
      if (this.num >= 1) this.num -= 1
    },
  },
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      console.log(value)
      value = value.toString()
      // 实例 字符串第一个字母转为大写
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
}
/**  
 *               跑马灯函数
 * @param a ul的class 必须写成字符串 -> 'txt'
 * @param b li的class 必须写成字符串 -> 'txt'
 * @param t 时间 单位毫秒 速率 1/t(px/毫秒) 默认 10 最佳
 * @param d direction 轮播方向 L -> left R -> right 必须写成字符串 -> 'txt'
 * 注意：css不要写ul的左或右绝对定位
 */
var runBox = function(a,b,t,d) {
  var oUl = document.getElementsByClassName(a)[0];
  var lis = oUl.getElementsByClassName(b);
    oUl.innerHTML += oUl.innerHTML;
    oUl.style.width = lis.length * lis[0].offsetWidth + 'px';
  if(d === 'L'){
    var l = null;
    var timer = function (){
      l -= 1;
      if( l< -oUl.offsetWidth / 2){
        l = 0;
      }
      oUl.style.left = l + 'px'
    };
  } else {
    var r = null;
    var timer = function (){
      r -= 1;
      if( r < -oUl.offsetWidth / 2){
        r = 0;
      }
      oUl.style.right = r + 'px'
    };
  }
  var play = setInterval(timer,t);
  oUl.onmouseover = function () { clearInterval(play) };
  oUl.onmouseout = function () { 
    play = setInterval( timer , t);
  }
}
/**
 * 跑马灯函数
 * @param t 时间速度 默认 10 最佳
 */
window.onload = function(){
  runBox('box','pic',10,'L');
  // lis[0].onmouseover = function(){
  //   console.log(1);
  // } 
  // for(var i = 0 ; i < lis.length ; i ++ ){
  //   lis[i].addEventListener("onmouseover",liseEven); 

  //   function liseEven(i){
  //     console.log(i);
  //   }
    // lis[i].onmouseover = function(){

      // for(var j = 0 ; j < 12 ; j ++ ){
      //   if( i === j ){
      //     lis[j].onmouseover = function(){
      //       console.log(j);
      //     }
      //   }
      // }
    // } 
  // }
  
} 

</script>