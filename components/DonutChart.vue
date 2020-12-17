<template>
  <div id="chart" class="p-4 text-left">
    <client-only>
      <apexchart
        type="donut"
        height="380"
        :options="chartOptions"
        :series="series"
      ></apexchart>
    </client-only>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    series: {
      type: Array,
      default: () => []
    },
    labels: {
      type: Array,
      default: () => []
    },
    totalLabel: {
      type: String,
      default: "Total"
    }
  },
  data() {
    return {
      chartOptions: {
        colors: ["#c4366f", "#85adff", "#502579"],
        legend: {
          position: "right",
          horizontalAlign: "left",
          fontWeight: 600,
          width: 160,
          onItemHover: {
            highlightDataSeries: true
          }
        },
        dataLabels: {
          enabled: false
        },
        plotOptions: {
          pie: {
            donut: {
              labels: {
                show: true,
                name: {
                  show: true,
                  offsetY: 12
                },
                value: {
                  offsetY: -24,
                  fontSize: "18px",
                  fontFamily: "Helvetica, Arial, sans-serif",
                  fontWeight: 600,
                  show: true
                },
                total: {
                  show: true,
                  label: this.totalLabel.toUpperCase(),
                  fontSize: "14px",
                  fontFamily: "sans-serif",
                  fontWeight: 600,
                  formatter: function(w: any) {
                    return (
                      w.globals.seriesTotals.reduce((a: number, b: number) => {
                        return a + b;
                      }, 0) + "%"
                    );
                  }
                }
              }
            }
          }
        },

        labels: this.labels,
        chart: {
          type: "donut"
        },
        responsive: [
          {
            breakpoint: 480,
            options: {
              legend: {
                position: "bottom"
              }
            }
          }
        ]
      }
    };
  }
});
</script>

<style>
#chart .apexcharts-legend-marker {
  margin-right: 8px !important;
}
.chart-loading {
  height: 380px;
}
</style>
