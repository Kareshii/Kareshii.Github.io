<template>
  <div id="app">
    <el-container>
      <el-header>
        <el-row :gutter="10">
          <el-col :xs="0" :sm="0" :md="0" :lg="0" :xl="0"></el-col>
          <el-col :xs="0" :sm="0" :md="0" :lg="0" :xl="0"></el-col>

          <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
            <el-menu
              :default-active="activeIndex"
              class="el-menu-demo"
              mode="horizontal"
              @select="handleSelect"
            >
              <el-menu-item index="1">彼氏</el-menu-item>
              <el-submenu index="2">
                <template slot="title">鱼</template>
                <el-menu-item index="2-1">选项1</el-menu-item>
                <el-menu-item index="2-2">选项2</el-menu-item>
                <el-menu-item index="2-3">选项3</el-menu-item>
                <el-submenu index="2-4">
                  <template slot="title">选项4</template>
                  <el-menu-item index="2-4-1">选项1</el-menu-item>
                  <el-menu-item index="2-4-2">选项2</el-menu-item>
                  <el-menu-item index="2-4-3">选项3</el-menu-item>
                </el-submenu>
              </el-submenu>
              <el-menu-item index="3">照片墙</el-menu-item>
            </el-menu>
          </el-col>
        </el-row>
      </el-header>
      <el-main>
        <!-- 轮播开始 -->
        <el-carousel height="600px">
          <el-carousel-item v-for="item in 4" :key="item">
            <h3>11111111111111</h3>
          </el-carousel-item>
        </el-carousel>

        <!-- 循环数据库卡片 -->
        <el-row :gutter="20">
          <el-col :span="4">&nbsp;</el-col>
          <el-col :span="16">
            <el-card
              class="box-card"
              shadow="hover"
              style="margin-top:60px;"
              v-for="i in 3"
              :key="i"
            >
              <img src="./assets/logo.png" class="image">
              <!-- <div v-for="o in 4" :key="o" class="text item">{{'列表内容 ' + o }}</div> -->
              <!-- {{ `和亲爱的宝贝已经在一起 ${day}天 ${hr}时 ${min}分 ${sec}秒` }} -->
              <time class="time">{{ currentDate }}</time>
            </el-card>
          </el-col>

          <el-col :span="4">&nbsp;</el-col>
        </el-row>
      </el-main>
      <el-footer>Footer</el-footer>
    </el-container>
  </div>
</template>

<script>
import moment from "moment";
export default {
  data() {
    return {
      activeIndex: "1",
      activeIndex2: "1",
      currentDate: "",
      day: "",
      hr: "",
      min: "",
      sec: ""
    };
  },
  created() {},
  watch: {},
  mounted() {
    this.getCurrentDateTime();
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    },
    getCurrentDateTime() {
      var vm = this;
      // const end = Date.parse(new Date("2019-01-04"));
      const end = Date.parse(
        moment("20190104013147", "YYYYMMDDhhmmss").format()
      );
      const now = Date.parse(new Date());
      const msec = parseInt((now - end) / 1000);
      let day = parseInt(msec / (24 * 60 * 60));
      let hr = parseInt((msec / (60 * 60)) % 24);
      let min = parseInt((msec / 60) % 60);
      let sec = parseInt(msec % 60);
      this.day = day;
      this.hr = hr > 9 ? hr : "0" + hr;
      this.min = min > 9 ? min : "0" + min;
      this.sec = sec > 9 ? sec : "0" + sec;
      setInterval(function() {
        vm.currentDate = moment().format();
        vm.getCurrentDateTime();
      }, 1000);
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
a {
  text-decoration: none;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.el-carousel__item h3 {
  color: #475669;
  font-size: 18px;
  opacity: 0.75;
  line-height: 600px;
  margin: 0;
}

.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}

/* 卡片样式 */
.text {
  font-size: 14px;
}

.item {
  margin-bottom: 18px;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}
.time {
  font-size: 13px;
  color: #999;
}
</style>
