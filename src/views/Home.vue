<template>
  <highcharts
    class="stock"
    :constructor-type="'stockChart'"
    :options="performanceTimeline"
  ></highcharts>
</template>

<script lang="ts">
import Vue from "vue";
import Highcharts from "highcharts";
import Component from "vue-class-component";

@Component
export default class OverTimeChart extends Vue {
  results: number[] = [1, 2, 3, 4, 5];

  get performanceTimeline() {
    let ctx = this,
      chartConfig: Highcharts.Options = {
        rangeSelector: {
          selected: 1
        },
        title: {
          text: "Performance Over Time"
        },
        yAxis: {
          labels: {
            formatter: function(
              this: Highcharts.AxisLabelsFormatterContextObject
            ): string {
              let labels = ["a", "b", "c", "d", "e"];
              let current: number = this.value;
              return labels[current];
            }
          }
        },
        tooltip: {
          formatter: function(
            this: Highcharts.TooltipFormatterContextObject
          ): string {
            return "<b>Status:</b> " + this.y;
          }
        },
        series: [
          {
            type: "line",
            name: "Status",
            step: "left",
            data: this.results.map(test => {
              return [1580315144 + 86000 * test * 1000, test];
            }),
            pointInterval: 1000 * 3600 * 24
          }
        ]
      };

    return chartConfig;
  }
}
</script>
