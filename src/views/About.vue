<template>
  <div class="about">
    <h1>关于我</h1>
    <el-divider></el-divider>
    <p><b>一蓑烟雨任平生</b></p>
    <el-divider></el-divider>
    <p><b>本人是来自重庆的在校大学生一枚，如果你也喜欢编程开发，欢迎一起来探讨研究♥</b></p>
    <img :src="require('../assets/img/mmqrcode1685275509471.png')" alt="图片" width="250px">
    <el-timeline>
      <el-timeline-item
          v-for="(item, index) in timelineData"
          :key="index"
          :timestamp="item.date"
      >
        <h3>{{ item.title }}</h3>
        <p>{{ item.content }}</p>
      </el-timeline-item>
    </el-timeline>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timelineData: [
        // 在这里添加您的时间轴数据
      ],
    };
  },
};
</script>

<style scoped>
.about {
  text-align: center;
  padding: 2rem;
}
</style>
