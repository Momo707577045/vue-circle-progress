<!--用户基本信息页面-->
<style scoped lang="scss">
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
    text-align: center;
    border-radius: 4px;
    background-color: #3D8AC7;
  }
}
</style>
<template>
  <section class="p-test">
    <circle-progress
      v-if="isShow"
      ref="$circle"
      class="progress"
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
        <input v-model="width" id="width" type="number" placeholder="例如：140"></li>
      <li>
        <label for="radius">进度条宽度（px）:</label>
        <input v-model="radius" id="radius" type="number" placeholder="例如：12"></li>
      <li>
        <label for="progress">进度百分比:</label>
        <input v-model="progress" id="progress" type="text" placeholder="例如：70"></li>
      <li>
        <label for="barColor">进度条颜色:</label>
        <input v-model="barColor" id="barColor" type="text" placeholder="例如：#f5a623"></li>
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
</template>
<script>

import CircleProgress from './components/circle-progress'

export default {
  components: {
    CircleProgress,
  },
  data() {
    return {
      isShow: true,
      width: 200,
      radius: 20,
      progress: 70,
      duration: 1000,
      delay: 20,
      barColor: '#F2AE57',
      backgroundColor: '#FFE8CC',
      timeFunction: 'cubic-bezier(0.99, 0.01, 0.22, 0.94)',
    }
  },

  methods: {
    reset() {
      this.isShow = false
      this.$nextTick(() => {
        this.isShow = true
      })
    }
  }
}

</script>
