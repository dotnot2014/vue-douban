<template>
  <div class="hello">
    <div>
        <span>{{msg}}</span><br>
        <button @click="getdata">获取数据</button>
        <br>
        <span>-----------------------------------</span>
    </div>
    <div class="content">
        <ul>
            <li v-for="(item, index) in articles" >
              <span class="myspan">
                <a :href="item.alt">{{ index+1 }} : {{ item.title }} ( {{ item.year }} )</a>
              </span>
              <span>
                <a :href="item.alt">
                  <img :src="item.images.large" :alt="item.title" >
                </a>
              </span>
            </li>
        </ul>
    </div>
  </div>
</template>


<script>
import reqwest from "reqwest"

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Top250-豆瓣电影',
      articles: [
        {
          title:"这是文章标题列表",
          year:2016,
          images:{large:"../static/logo.png"},
          alt:"http://www.douban.com"

        }
      ]
    }
  },
  methods: {
    getdata: function (e) {
      var that = this
      reqwest({
        //url: "https://cnodejs.org/api/v1/topics",
        url:"http://api.douban.com/v2/movie/top250",
        method: "get",
        type: 'jsonp',
        data: {},
        success(res) {
          that.articles = res.subjects
          console.log(res.subjects)
          console.log("数据加载完毕...")
        },
        error(err) {
          console.log(err)
        }
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.content{
  margin:0 auto;
  width:500px;
}
ul {
  list-style-type: none;
  padding: 0;
  text-align: center;
}

li{
  padding-top:10px;
}

a {
  color: #42b983;
  text-decoration:none; 
}
.myspan{
  margin:0 auto;
  display:block;
  width:300px;
  text-align:left;
}
</style>
