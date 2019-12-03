<template>
  <div class="container">
    <div class="input-wrapper">
      <select-input :menus="menus" @select="select($event)" />
      <label class="checkbox">
        <input @click="check" :checked="checked" type="checkbox" />
        アノテーションを付与
      </label>
    </div>
    <template v-if="!checked">
      <chart
        :chartType="chartType"
        :chartData="chartData"
        :chartOptions="chartOptions"
      />
    </template>
    <template v-else>
      <chart-with-annotation
        :chartType="chartType"
        :chartData="chartData"
        :chartOptions="chartOptions"
      />
    </template>
  </div>
</template>

<script>
import Chart from '@/components/atoms/Chart.vue'
import ChartWithAnnotation from '@/components/atoms/ChartWithAnnotation.vue'
import SelectInput from '@/components/atoms/SelectInput.vue'

export default {
  components: {
    Chart,
    ChartWithAnnotation,
    SelectInput
  },
  data() {
    return {
      chartType: 'PieChart',
      chartData: [
        ['年', 'A商品', 'B商品', 'C商品'],
        ['2014', 1000, 400, 200],
        ['2015', 1170, 460, 250],
        ['2016', 660, 1120, 300],
        ['2017', 1030, 540, 350]
      ],
      chartOptions: {
        title: '会社の売上（商品別）',
        subtitle: '売上',
        width: 800,
        height: 800,
        isStacked: 'percent'
      },
      menus: [
        {
          name: '縦棒グラフ',
          value: 'ColumnChart'
        },
        {
          name: '円グラフ',
          value: 'PieChart'
        },
        {
          name: '棒グラフ',
          value: 'BarChart'
        }
      ],
      checked: false
    }
  },
  methods: {
    select(e) {
      this.checked = false
      this.chartType = e
    },
    check() {
      this.checked = !this.checked
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  flex-direction: column;
}
.input-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
}
</style>
