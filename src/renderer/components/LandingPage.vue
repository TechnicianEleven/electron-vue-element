<template>
  <div id="wrapper">
    <div class="timelist">
      <div class="timeTitle">
        <el-tag @click="showTip">開始時間(start)</el-tag> 
        -
        <el-tag @click="showTip">結束時間(end)</el-tag>
      </div>
      <div class="item" v-for="(item,i) in timeList" :key="i">
       <el-tag type='success' @click="showTip"  effect="plain">{{Object.keys(item)[0]}}</el-tag> - <el-tag @click="showTip" type='success'  effect="plain">{{Object.values(item)[0]}}</el-tag>
      </div>
    </div>
    <div class="footer-creator">
      creator-by-CND產品處 
    </div>
  </div>
</template>

<script>
// import Vue from 'vue'
let fs = require('fs')
export default {
  data () {
    return {
      timeList: []
    }
  },
  methods: {
    showTip () {
      this.$message({
        'message': '沒有修改權限，請聯繫管理員!',
        'duration': '1000',
        'type': 'warning'
      })
    }
  },
  created () {
    // console.log('dddd')
    let that = this
    fs.readFile('./DefaultConfig.json', 'utf-8', (err, data) => {
      if (err) {
        console.log(err)
        return 'err'
      } else {
        that.timeList = JSON.parse(data)['TimeList']
      }
    })
  }
  // watch: {
  //   form (newTime, oldTime) {
  //     console.log(123)
  //   }
  // }
}
</script>

<style  scope lang="scss">
#wrapper{
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  .el-tag{
    cursor: pointer;
  }
  .footer-creator{
    position: absolute;
    width: 120px;
    bottom: 2px;
    right: 10px;
    color:goldenrod;
    text-shadow: 2px 2px 2px;
    font-size: 10px;
    font-style:italic;
  }
  .timelist{
  color:#666;
  // display: flex;
  // justify-content: center;
  // align-items: center;
  .timeTitle{
    margin: 20px;
    .el-tag{
      width: 200px;
      height: 40px;
      line-height: 40px;
      text-align: center;
      font-size: 14px;
      cursor: pointer;

    }
  }

}
.item{
  text-align: center;
  span{
    margin: 5px;
  }
}
}

</style>
