<script>
import Vue3ChartJs from "@j-t-mcc/vue3-chartjs";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    Vue3ChartJs,
  },
  setup() {
    const chartRef = ref(null);
    const lineChart = {
      type: "line",
      data: {
        labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul"],
        datasets: [
          {
            label: "Revenue",
            data: [65, 59, 80, 81, 56, 55, 40],
            fill: false,
            borderColor: "orange",
            tension: 0,
            backgroundColor: "white",
          },
          {
            label: "Total Cost",
            data: [70, 25, 110, 90, 5, 60, 30],
            fill: false,
            borderColor: "#5b99e6",
            tension: 0,
            backgroundColor: "white",
          },
        ],
      },
    };

    const exportChart = () => {
      let a = document.createElement("a");
      a.href = chartRef.value.chartJSState.chart.toBase64Image();
      a.download = "image-export.png";
      a.click();
      a = null;
    };

    return {
      chartRef,
      lineChart,
      exportChart,
    };
  },
};
</script>

<template>
  <div class="section">
    <div class="card">
      <h3>Profit-Loss</h3>
      <button type="submit" @click="exportChart">Export Chart as PNG</button>
      <div class="line-container">
        <vue3-chart-js ref="chartRef" v-bind="{ ...lineChart }" class="line" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.section {
  width: 100%;
  background: none;
  color: var(--general);
  margin-top: 3rem;
}

h3 {
  margin-bottom: 1.75rem;
}

.card {
  width: 100%;
  background-color: var(--light);
  padding: 2rem;
  border-radius: 0.5rem;
  box-shadow: 0 1px 12px 1px var(--based);
  border-top: 2px solid var(--blue);
}

.line-container {
  display: flex;
  align-items: center;
  justify-content: center;
}

.line {
  max-width: 60vw;
  max-height: 40vh;
}

button {
  background-color: var(--blue);
  padding: 0.5rem 1.5rem;
  color: var(--light);
  font-size: 1rem;
  font-weight: bold;
  border-radius: 0.5rem;
  border: 2px solid var(--base);
  top: 0;
  right: 0;
}

button:hover {
  filter: opacity(95%);
}
</style>
