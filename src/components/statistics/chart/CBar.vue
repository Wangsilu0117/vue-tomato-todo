<template>
  <div
    ref="chartContainer"
    class="bar-container"
  >
    <v-chart
      id="bar"
      ref="chart"
      :init-options="chartInitOptions"
      :options="chartOptions"
      autoresize
      theme="roma"
    />
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Object,
      default: null
    },
    notMerge: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      chartInitOptions: {},
      chartOptions: {
        title: {
          text: ''
        },
        tooltip: {
          trigger: 'item',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow', // 默认为直线，可选为：'line' | 'shadow',
            shadowStyle: {}
          },
          textStyle: {
            fontSize: 10
          }
        },
        legend: {
          left: 'center',
          data: [],
          bottom: 0,
          padding: 0,
          itemGap: 0,
          itemWidth: 8,
          itemHeight: 8,
          selectedMode: false,
          formatter: () => '',
          textStyle: {
            fontSize: 9,
            color: '#555'
          }
        },
        grid: {
          top: '10%',
          left: '0%',
          right: '4%',
          bottom: '12%',
          containLabel: true
        },
        xAxis: [
          {
            type: 'category',
            splitLine: {
              show: false
            },
            axisLabel: {
              fontSize: 10
            },
            axisTick: {
              show: false,
              alignWithLabel: true
            },
            axisLine: {
              show: false,
              lineStyle: {
                color: '#555'
              }
            }
          }
        ],
        yAxis: [
          {
            type: 'value',
            splitLine: {
              show: false
            },
            axisLabel: {
              fontSize: 10,
              color: '#555',
              formatter: `{value} ${this.$t('word.minute')}`
            },
            axisTick: {
              show: false,
              alignWithLabel: true
            },
            axisLine: {
              show: false,
              lineStyle: {
                color: '#555'
              }
            }
          }
        ],
        series: [
          {
            name: '',
            type: 'bar',
            barCategoryGap: '3',
            label: {
              show: true,
              position: 'top',
              fontSize: 8
            },
            emphasis: {},
            data: []
          }
        ],
        textStyle: {
          color: '#555'
        },
        animationDuration: 2000
      }
    }
  },
  watch: {
    options (val) {
      if (!_isEmpty(val)) {
        if (!this.notMerge) {
          this.chartOptions = val
          return
        }
        Object.assign(this.chartOptions, val)
      }
    }
  }
}
</script>

<style lang="less">
.bar-container {
  width: 100%;
  height: 3rem;
}
</style>
