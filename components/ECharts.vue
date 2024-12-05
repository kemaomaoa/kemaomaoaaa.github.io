<template>
  <div ref="echarts" style="width: 100%; height: 400px;"></div>
</template>

<script>
import * as echarts from 'echarts'

export default {
  name: 'ECharts',
  props: {
    options: {
      type: Object,
      default: () => ({})
    }
  },
  mounted() {
    this.initECharts();
  },
  methods: {
    initECharts() {
      this.chart = echarts.init(this.$refs.echarts);
      this.chart.setOption(this.options);
    }
  },
  watch: {
    options: {
      deep: true,
      handler(newVal) {
        this.chart.setOption(newVal);
      }
    }
  },
  // 使用 beforeUnmount 替换 beforeDestroy
  beforeUnmount() {
    if (this.chart) {
      this.chart.dispose();
    }
  }
}
</script>