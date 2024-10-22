<script>
    import { onMount } from 'svelte';
    // @ts-ignore
    import Chart from 'chart.js/auto';
  
    let sleepData = [];
    let heartRateData = [];
    let avgSleep = 0;
    let avgHeartRate = 0;
    let sleepChart;
    let heartRateChart;
  
 
    const sleepHours = [7, 8, 6, 5.5, 7.5, 6.5, 8]; 
    const heartRates = [72, 75, 70, 80, 74, 78, 76]; 
  
    onMount(() => {
      sleepData = sleepHours; 
      heartRateData = heartRates; 
      avgSleep = sleepHours.reduce((a, b) => a + b) / sleepHours.length;
      avgHeartRate = heartRates.reduce((a, b) => a + b) / heartRates.length;
  
      const sleepCtx = document.getElementById('sleepChart').getContext('2d');
      sleepChart = new Chart(sleepCtx, {
        type: 'bar',
        data: {
          labels: ['Day 1', 'Day 2', 'Day 3', 'Day 4', 'Day 5', 'Day 6', 'Day 7'],
          datasets: [{
            label: 'Hours of Sleep',
            data: sleepData,
            backgroundColor: 'rgba(75, 192, 192, 0.2)',
            borderColor: 'rgba(75, 192, 192, 1)',
            borderWidth: 1
          }]
        },
        options: {
          scales: {
            y: {
              beginAtZero: true,
              suggestedMax: 10
            }
          }
        }
      });

      const heartRateCtx = document.getElementById('heartRateChart').getContext('2d');
      heartRateChart = new Chart(heartRateCtx, {
        type: 'line',
        data: {
          labels: ['Day 1', 'Day 2', 'Day 3', 'Day 4', 'Day 5', 'Day 6', 'Day 7'],
          datasets: [{
            label: 'Heart Rate (bpm)',
            data: heartRateData,
            backgroundColor: 'rgba(255, 99, 132, 0.2)',
            borderColor: 'rgba(255, 99, 132, 1)',
            borderWidth: 1,
            fill: false
          }]
        },
        options: {
          scales: {
            y: {
              beginAtZero: true,
              suggestedMax: 100
            }
          }
        }
      });
    });
  

    function destroyCharts() {
      if (sleepChart) {
        sleepChart.destroy();
      }
      if (heartRateChart) {
        heartRateChart.destroy();
      }
    }
</script>

<style>
  .health-container {
    padding: 20px;
    margin-top: 20px;
    background-color: #f4f4f4;
    border-radius: 10px;
    box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.1);
  }

  .avg-metrics {
    font-size: 1.2rem;
    margin-top: 10px;
  }

  .chart {
    margin-top: 20px;
  }
</style>

<div class="health-container">
  <h3>Health and Sleep Stats</h3>
  <p class="avg-metrics">Average Sleep: {avgSleep.toFixed(1)} hours per night</p>
  <div class="chart">
    <canvas id="sleepChart" width="400" height="200"></canvas>
  </div>

  <p class="avg-metrics">Average Heart Rate: {avgHeartRate.toFixed(1)} bpm</p>
  <div class="chart">
    <canvas id="heartRateChart" width="400" height="200"></canvas>
  </div>
</div>
