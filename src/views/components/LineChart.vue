<script>
import { Line, Bar } from "vue-chartjs";

let linechart = [];
let barchart = [];
for (var i = 0; i < 31; i++) {
  barchart[i] = 4.8;
}
linechart[0] = 10;
for (var j = 1; j < 21; j++) {
  linechart[j] = linechart[j - 1] + j / 30;
}
for (var k = 21; k < 31; k++) {
  linechart[k] = linechart[k - 1] + k / 25;
}

export default {
  extends: Bar,
  data() {
    return {
      chartData: {
        labels: [
          "0",
          "",
          "",
          "1",
          "",
          "",
          "2",
          "",
          "",
          "3",
          "",
          "",
          "4",
          "",
          "",
          "5",
          "",
          "",
          "6",
          "",
          "",
          "7",
          "",
          "",
          "8",
          "",
          "",
          "9",
          "",
          "",
          "10",
        ],
        datasets: [
          {
            type: "line",
            label: "Yield",
            data: linechart,
            yAxisID: "yAxis1",
            fill: false,
            borderColor: "#FFFFFF",
            backgroundColor: "#2554FF",
            borderWidth: 5,
          },
          {
            type: "bar",
            label: "Stake",
            data: barchart,
            fill: false,
            borderColor: "#6d1eda",
            backgroundColor: "#6d1eda",
          },
        ],
      },
      options: {
        // plugins: {
        //   subtitle: {
        //     display: true,
        //     text: "Custom Chart Subtitle",
        //   },
        // },
        elements: {
          point: {
            radius: 0,
          },
        },
        bezierCurve: true,
        scales: {
          yAxes: [
            {
              id: "yAxis1",
              ticks: {
                beginAtZero: true,
                callback: (value, index, values) => {
                  return `${value}.00%`;
                },
                fontColor: "white",
              },
              gridLines: {
                display: true,
                color: "gray",
                lineWidth: 3,
              },
              scaleLabel: {
                display: true,
                labelString: "Annualised Yield",
                fontColor: "white",
              },
            },
            {
              id: "yAxis2",
              type: "category",
              position: "right",
              gridLines: {
                drawOnChartArea: true, // only want the grid lines for one axis to show up
              },
              scaleLabel: {
                display: true,
                labelString: "Stake %",
                fontColor: "white",
              },
              min: 0,
              max: 10,
              ticks: {
                reverse: true,
                maxTicksLimit: 10,
                callback: (value, index, values) => {
                  return `${value}.00%`;
                },
                fontColor: "white",
              },
            },
          ],
          xAxes: [
            {
              barThickness: 8 ,
              gridLines: {
                display: false,
              },
              scaleLabel: {
                display: true,
                labelString: "Stake Maturity (Years)",
                fontColor: "white",
              },
              ticks: {
                callback: function (value, index, ticks) {
                  return value;
                },
                fontColor: "white",
                rotation: 20
              },

            },
          ],
        },
        legend: {
          display: false,
          // position: "bottom",
          // padding: "10",
          // align: 'left'
        },
        tooltips: {
          callbacks: {
            title: function (tooltipItem, data) {
              return "";
            },
            label: function (tooltipItem, data) {
              return "";
            },
            afterLabel: function (tooltipItem, data) {
              return "\nMaturrity  JAN-2026 \n\n      Yield  JAN-2026\n";
            },
          },
        },
        onHover: (event, chartElement) => {
          event.target.style.cursor = chartElement[0] ? 'pointer' : 'default';
        },
        responsive: true,
        maintainAspectRatio: false,
      },
    };
  },
  mounted() {
    this.renderChart(this.chartData, this.options);
  },
};
</script>