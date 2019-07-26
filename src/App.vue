<!--用户基本信息页面-->
<style scoped lang="scss">
.p-switch {
  position: fixed;
  right: 100px;
  top: 20px;
  margin: 30px auto 0;
  width: 200px;
  height: 40px;
  color: white;
  cursor: pointer;
  line-height: 40px;
  font-size: 20px;
  text-align: center;
  border-radius: 4px;
  background-color: #3D8AC7;
  z-index: 2;
}
.p-test {
  padding: 60px;
  text-align: center;
  background-color: white;
  ul {
    position: fixed;
    padding: 30px 20px;
    top: 50px;
    left: 50px;
    text-align: center;
    font-weight: bold;
    border-radius: 10px;
    background-color: rgba(0, 0, 0, 0.1);
  }
  li {
    margin-top: 14px;
    font-size: 16px;
    list-style: none;
  }
  li:nth-child(1) {
    margin: 0
  }
  label {
    display: inline-block;
    width: 140px;
    height: 24px;
    line-height: 24px;
    text-align: left;
  }
  input {
    display: inline-block;
    padding: 0 10px;
    width: 150px;
    height: 24px;
    outline: none;
    font-size: 14px;
    border: solid 1px gray;
    border-radius: 2px;
    text-decoration: none;
    &:hover {outline: none;}
  }
  .btn {
    margin: 30px auto 0;
    width: 200px;
    height: 40px;
    color: white;
    line-height: 40px;
    font-size: 20px;
    cursor: pointer;
    text-align: center;
    border-radius: 4px;
    background-color: #3D8AC7;
  }
}
.p-duration-model {
}
</style>
<template>
  <section>
    <section class="p-switch btn" @click="isDurationModel=!isDurationModel">{{isDurationModel ? '动画模式': '持续模式'}}</section>
    <section class="p-test" v-if="!isDurationModel">
      <circle-progress
        v-if="isShow"
        ref="$circle"
        class="progress"
        key="animation-model"
        :isAnimation="true"
        :isRound="true"
        :width="width"
        :radius="radius"
        :progress="progress"
        :barColor="barColor"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      >
      </circle-progress>
      <ul>
        <li>
          <label for="width">圆宽（px）:</label>
          <input v-model="width" id="width" type="number" placeholder="例如：140">
        </li>
        <li>
          <label for="radius">进度条宽度（px）:</label>
          <input v-model="radius" id="radius" type="number" placeholder="例如：12">
        </li>
        <li>
          <label for="progress">进度百分比:</label>
          <input v-model="progress" id="progress" type="text" placeholder="例如：70">
        </li>
        <li>
          <label for="barColor">进度条颜色:</label>
          <input v-model="barColor" id="barColor" type="text" placeholder="例如：#f5a623">
        </li>
        <li>
          <label for="backgroundColor">背景颜色:</label>
          <input v-model="backgroundColor" id="backgroundColor" type="text" placeholder="例如：#FFE8CC">
        </li>
        <li>
          <label for="duration">动画时长（ms）:</label>
          <input v-model="duration" id="duration" type="number" placeholder="例如：1000">
        </li>
        <li>
          <label for="delay">延迟执行（ms）:</label>
          <input v-model="delay" id="delay" type="number" placeholder="例如：20">
        </li>
        <li>
          <label for="timeFunction">缓动算法:</label>
          <input v-model="timeFunction" id="timeFunction" type="text" placeholder="例如：cubic-bezier(0.99, 0.01, 0.22, 0.94)">
        </li>
        <li>
          <div class="btn" @click="reset">重置动画</div>
        </li>
      </ul>
    </section>
    <section class="p-test p-duration-model" v-else>
      <circle-progress
        v-if="isShow"
        ref="$circle"
        class="progress"
        key="duration-model"
        :isAnimation="false"
        :isRound="true"
        :width="width"
        :radius="radius"
        :progress="currentTime / durationTime * 100"
        :barColor="barColor"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      >
      </circle-progress>
      <ul>
        <li>
          <label for="width">圆宽（px）:</label>
          <input v-model="width" type="number" placeholder="例如：140">
        </li>
        <li>
          <label for="radius">进度条宽度（px）:</label>
          <input v-model="radius" type="number" placeholder="例如：12">
        </li>
        <li>
          <label for="barColor">进度条颜色:</label>
          <input v-model="barColor" type="text" placeholder="例如：#f5a623">
        </li>
        <li>
          <label for="backgroundColor">背景颜色:</label>
          <input v-model="backgroundColor" type="text" placeholder="例如：#FFE8CC">
        </li>
        <li>
          <label for="duration">总时长（s）:</label>
          <input v-model="durationTime" type="number" placeholder="例如：1000">
        </li>
        <li>
          <label for="duration">当前时长（s）:</label>
          <input v-model="currentTime.toFixed(2)" type="number" style="color: #aaaaaa;border-color: #aaaaaa" disabled placeholder="例如：1000">
        </li>
        <li>
          <div class="btn" @click="startTime">{{currentTime > 0 ? '重新计时' : '开始计时'}}</div>
        </li>
      </ul>
    </section>
  </section>
</template>
<script>

import CircleProgress from './components/circle-progress'

export default {
  components: {
    CircleProgress,
  },
  data() {
    return {
      isDurationModel: true, // 是否打开持续缓动模式
      isShow: true,
      width: 200,
      radius: 20,
      progress: 70,
      duration: 1000,
      delay: 20,
      barColor: '#F2AE57',
      backgroundColor: '#FFE8CC',
      timeFunction: 'cubic-bezier(0.99, 0.01, 0.22, 0.94)',

      intervalTimer: null, // 持续模式，循环计时器
      currentTime: 0, // 当前时间
      durationTime: 60, // 持续模式总时长
    }
  },

  watch: {
    isDurationModel() {
      clearInterval(this.intervalTimer)
      this.currentTime = 0
    }
  },

  methods: {
    // 重置动画
    reset() {
      this.isShow = false
      this.$nextTick(() => {
        this.isShow = true
      })
    },

    // 开始计时
    startTime() {
      let spaceTime = 10;
      clearInterval(this.intervalTimer)
      this.currentTime = 0
      this.intervalTimer = setInterval(() => {
        this.currentTime += spaceTime / 1000
        if (this.currentTime >= this.durationTime) {
          clearInterval(this.intervalTimer)
        }
      }, spaceTime)
    }
  }
}

</script>
