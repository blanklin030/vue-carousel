<template>
  <div class="blank">
    <div class="btn">
      <button @click="handleClear">
        {{this.timer ? '停止滚动': '自动滚动'}}
      </button>
      <button @click="autoLoop">滚动设定</button><input v-model="second" placeholder="请输入秒数"/>
    </div>
    <div class="app">
      <div class="left"><img src="./assets/left.png" @click="handleLeft"/></div>

      <div class="carousel">
        <div class="container" :style="{left:left+'px'}">
          <div 
            @mouseover="handleClear" 
            @mouseleave="autoLoop"
            v-for="(item,key) in list" 
            :key="key" 
            class="item">
            index {{item}}
          </div>
        </div>
      </div>

      <div class="right"><img src="./assets/right.png" @click="handleRight" /></div>

    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      left: 0,
      timer: null,
      len: 10,
      list: [],
      second: 1
    }
  },
  mounted() {
    this.initData()
    this.autoLoop();
  },
  methods: {
    handleClear() {
      clearInterval(this.timer)
      this.timer = null
    },
    initData() {
      for (let index = 0; index < this.len; index++) {
        this.list.push(index+1)
      }
    },
    autoLoop() {
       this.timer = setInterval(()=>{
          this.handleRight()
        }, parseInt(this.second) * 1000)
    },
    handleLeft() {
      if(this.left == 0){
        this.left = -(this.len-3)*210;
      }else {
        this.left += 210
      }
    },
    handleRight() {
      if (this.left == -(this.len-3)*210){
        this.left = 0
      } else {
        this.left -= 210
      }
    }
  },
}
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
  text-decoration: none;
}
body {
  padding: 0;
  margin: 0;
}

.btn {
  width: 300px;
  margin: 10px auto;
}

.app {
  width: 700px;
  height: 50px;
  display: flex;
  justify-content: space-between;
  border: 1px dashed #cccccc;
  padding: 5px;
  margin: 50px auto;
  overflow: hidden;
}

.left {
  background-color: rgba(0, 0, 0, .1);
  width: 25px;
  height: 25px;
  cursor: pointer;
  margin-top: 15px;
}
.left:hover {
  background-color: rgba(0, 0, 0, .5);
}
.left img {
  width: 20px;
}

.right {
  background-color: rgba(0, 0, 0, .1);
  width: 25px;
  height: 25px;
  cursor: pointer;
  margin-top: 15px;
}
.right:hover {
  background-color: rgba(0, 0, 0, .5);
  transition-timing-function: ease-in-out;
  transition-property: background-color;
  transition-duration: 100ms;
}
.right img {
  width: 20px;
}

.carousel {
  width: 85%;
  overflow: hidden;
  position: relative;
}

.container {
  width: 20000px;
  height: 50px;
  position: absolute;
  z-index: 1;
  transition-timing-function: ease-in-out;
  transition-property: left;
  transition-duration: 1000ms;
}
.item {
  width: 200px;
  height: 40px;
  background-color: #cccccc;
  margin: 5px;
  float: left;
  line-height: 40px;
  text-align: center;
}
</style>
