<template>
  <div>
    <apexchart
      width="500"
      type="line"
      :options="chartOptions"
      :series="series"
    ></apexchart>
  </div>
</template>

<script>
import VueApexCharts from "vue3-apexcharts";

export default {
  name: 'Chart',
  components: {
    apexchart: VueApexCharts,
  },
  props: ['data'],
  data: function() {
    return {
      series: [
        {
          name: "temperatures",
          data: this.data.map(a => Math.round(a.temp)+'°'),
        },
      ],
      chartOptions: {
            chart: {
              height: 350,
              type: 'line',
              dropShadow: {
                enabled: true,
                color: '#000',
                top: 18,
                left: 7,
                blur: 10,
                opacity: 0.2
              },
              toolbar: {
                show: false
              }
            },
            colors: ['#373e47', 'green'],
            dataLabels: {
              enabled: true,
            },
            stroke: {
              curve: 'smooth'
            },
            title: {
              text: 'Temperature for next 24 hours',
              align: 'left'
            },
            grid: {
              borderColor: '#6a6a7a',
              row: {
                colors: ['#1A1919'],
                opacity: 1,
              },
            },
            markers: {
              size: 1
            },
            xaxis: {
               categories: this.data.map(a => new Date(a.dt * 1000).getHours()+':00'),
              title: {
                text: 'Hour'
              }
            },
            yaxis: {
              title: {
                text: 'Temperature'
              },
              min: 5,
              max: 40
            },
            legend: {
              position: 'top',
              horizontalAlign: 'right',
              floating: true,
              offsetY: -25,
              offsetX: -5
            }
          },
    };
  },
};

</script>

<style>

</style>