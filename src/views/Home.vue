<template>
  <highcharts
    class="stock"
    :constructor-type="'stockChart'"
    :options="performanceTimeline"
  ></highcharts>
</template>

<script lang="ts">
import Vue from "vue";
import Component from "vue-class-component";

@Component
export default class OverTimeChart extends Vue {
  results: number[] = [1, 2, 3, 4, 5];

  get performanceTimeline() {
    var ctx = this;
    return {
      rangeSelector: {
        selected: 1
      },
      title: {
        text: "Performance Over Time"
      },
      yAxis: {
        labels: {
          formatter: function(): string {
            let labels = ["a", "b", "c", "d", "e"];
            let current: number = this.value;
            return labels[current];
          }
        }
      },
      tooltip: {
        formatter: function(): string {
          return "<b>Status:</b> " + this.y;
        }
      },
      series: [
        {
          name: "Status",
          step: true,
          data: this.results.map(test => {
            return [1580315144 + 86000 * test * 1000, test];
          }),
          pointInterval: 1000 * 3600 * 24
        }
      ]
    };
  }
}
</script>
