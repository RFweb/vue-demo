<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{ msg1 }}</h2>
    <div v-html="message"></div>

    <label for="r1">修改颜色</label><input type="checkbox" v-model="class1" id="r1">
    <br>
    <div v-bind:class="{'class1': class1}">
      directiva v-bind:class
    </div>

    {{5+5}}<br>
    {{ ok ? 'YES' : 'NO' }}<br>
    {{ message.split('').reverse().join('') }}
    <div v-bind:id="'list-' + id">今天
      <span v-if="rain===0">晴天</span>
      <span v-if="rain===1">下雨了</span>
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

  </div>
</template>

<script>
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
      rain: 0,
      url: 'http://www.baidu.com',
      inputTxt: 'Runoob!',
      num: 0
    }
  },
  methods: {
    numAdd: function () {
      this.num += 1
    },
    numReduce: function () {
      if (this.num >= 1) this.num -= 1
    }
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
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.class1{
  width: 100px;
  height: 100px;
  background: #ddd;
}
</style>
