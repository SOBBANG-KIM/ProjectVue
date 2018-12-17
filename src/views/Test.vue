<template>
  <div>
    <canvas id="planet-chart"></canvas>
     <table>
      <thead>
        <tr>
          <th>날짜</th>
          <th>시간</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="voc of vocData" v-bind:key="voc.key">
          <td>{{voc}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
    import {db} from '../firebase'
    import Chart from 'chart.js';
    import planetChartData from '../data/chart-data.js';

    export default {
        name: 'Test',
        firebase: {
            vocData: {
                source: db.ref('VOC_DATA'),
                cancelCallback(err) {
                    console.error(err);
                }
            }
        },
        data() {
          return {
              vocData:[],
              planetChartData: planetChartData,
          } 
        },
        methods: {
            createChart(chartId, chartData) {
                const ctx = document.getElementById(chartId);
                const myChart = new Chart(ctx, {
                type: chartData.type,
                data: chartData.data,
                options: chartData.options,
                });
            }
        },
        mounted() {
            this.createChart('planet-chart', this.planetChartData);
        }
    }
</script>

<style scoped>

</style>
