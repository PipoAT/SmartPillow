<script>
  import thermometer from "../assets/Thermometer.webp";
  // Declare a reactive variable for progress
  let setTemperature = 50;
  let temperature = 50;
  let tempStatus = "No Change";

  // Function to interpolate between colors representing temperature
  $: temperatureColor =
    temperature < 40
      ? // Below 40, keep it Blue (No color change)
        `rgb(0, 0, 255)`
      : temperature < 55
        ? // Interpolate from Blue (0, 0, 255) to Light Blue (0, 255, 255) between 40% and 55%
          `rgb(0, ${Math.round(255 * ((temperature - 40) / 15))}, 255)`
        : temperature < 70
          ? // Interpolate from Light Blue (0, 255, 255) to Yellow (255, 255, 0) between 55% and 70%
            `rgb(${Math.round(255 * ((temperature - 55) / 15))}, 255, ${255 - Math.round(255 * ((temperature - 55) / 15))})`
          : temperature < 80
            ? // Interpolate from Yellow (255, 255, 0) to Orange (255, 165, 0) between 70% and 80%
              `rgb(255, ${255 - Math.round(90 * ((temperature - 70) / 10))}, 0)`
            : // Interpolate from Orange (255, 165, 0) to Red (255, 0, 0) between 80% and 90%
              temperature <= 90
              ? `rgb(255, ${Math.round(165 - 165 * ((temperature - 80) / 10))}, 0)`
              : // Above 90, keep it Red (No color change)
                `rgb(255, 0, 0)`;

  let setFirmness = 50;
  let firmness = 50;
  let firmnessStatus = "No Change";

  function wait(ms) {
    return new Promise((resolve) => setTimeout(resolve, ms));
  }

  async function changeTemperature() {
    await wait(5000);
    while (temperature != setTemperature) {
      if (temperature < setTemperature) {
        tempStatus = "Warming Up...";
        temperature += 0.1;
        await wait(10);
      }
      else if (temperature > setTemperature) {
        tempStatus = "Cooling Down...";
        temperature -= 0.1;
        await wait(10);
      }
      temperature = Number(temperature.toFixed(1));
    }
    tempStatus = "No Change";
  }

  async function changeFirmness() {
    await wait(5000);
    console.log(setFirmness);
    while (firmness != setFirmness) {
      if (firmness < setFirmness) {
        firmnessStatus = "Hardening...";
        firmness += 0.1;
        await wait(10);
      }
      else if (firmness > setFirmness) {
        firmnessStatus = "Softening...";
        firmness -= 0.1;
        await wait(10);
      }
      firmness = Number(firmness.toFixed(1));
    }
    firmnessStatus = "No Change";
  }
</script>

<div class="comfortPage">
  <h1 class="header">Comfort</h1>
  <div class="mainContent">
    <div class="temperature">
      <h1>Temperature</h1>
      <div class="subContent">
        <div class="text">
          <h2>Current<br />Pillow<br />Temperature:<br />Status: {tempStatus}</h2>
        </div>
        <div class="value">
          <img class="tempImage" src={thermometer} />
          <div class="progress-bar">
            <!-- Gradient fill that dynamically changes width and color -->
            <div
              class="fill"
              style="width: {(temperature - 40) *
                2}%; background-color: {temperatureColor};"
            ></div>
          </div>
          <h2 class="tempText">{Math.round(temperature)}°</h2>
          <!--<progress class="tempProgress" style="--progress-color: {progressColor};" max="100" value={progress}></progress>-->
        </div>
      </div>
      <div class="subContent">
        <div class="text">
          <h2>Set<br />Pillow<br />Temperature:</h2>
        </div>
        <div class="value">
          <div class="progress-container">
            <!-- Range Slider to edit progress -->
            <input
              type="range"
              min="40"
              max="90"
              bind:value={setTemperature}
              on:change={changeTemperature}
            />

            <!-- Display the percentage -->
            <p>{setTemperature}°F</p>
          </div>
        </div>
      </div>
    </div>
    <div class="firmness">
      <h1>Firmness</h1>
      <div class="subContent">
        <div class="text">
          <h2>Current<br />Pillow<br />Firmness:<br />Status: {firmnessStatus}</h2>
        </div>
        <div class="value">
          <h1>{Math.round(firmness)}%</h1>
        </div>
      </div>
      <div class="subContent">
        <div class="text">
          <h2>Set<br />Pillow<br />Firmness:</h2>
        </div>
        <div class="value">
          <div class="progress-container">

            <!-- Range Slider to edit progress -->
            <input type="range" min="0" max="100" bind:value={setFirmness} on:change={changeFirmness}/>

            <!-- Display the percentage -->
            <p>{setFirmness}%</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  h1,
  h2,
  h3 {
    text-align: center;
  }

  .header {
    font-size: 48px;
  }

  .mainContent,
  .subContent {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
  }

  .subContent {
    height: 200px;
  }

  .temperature,
  .firmness,
  .text,
  .value {
    width: 50%;
  }

  .value {
    z-index: 0;
    position: relative;
  }

  .progress-container {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  progress {
    width: 100%;
    height: 20px;
    margin-bottom: 10px;
  }

  input[type="range"] {
    width: 100%;
  }

  .tempProgress {
    top: 97px;
    right: 82px;
    height: 55px;
    width: 230px;
    transform: rotate(270deg);
    position: absolute;
    z-index: -1;
    appearance: none;
  }

  .tempImage {
    height: 250px;
    width: auto;
    z-index: 100;
  }

  /* Style for the progress bar */
  progress::-webkit-progress-bar {
    background-color: #f3f3f3; /* Background color */
    border-radius: 25px;
    overflow: hidden;
  }

  /* Style for the value portion (Chrome/Safari) */
  progress::-webkit-progress-value {
    background-color: var(--progress-color); /* Green color for progress */
  }

  /* Custom progress bar styling */
  .progress-bar {
    top: 97px;
    left: 65px;
    height: 55px;
    width: 230px;
    transform: rotate(270deg);
    position: absolute;
    z-index: -1;
    background-color: #f3f3f3;
    border-radius: 25px;
    overflow: hidden;
  }

  /* The gradient fill div inside the progress bar */
  .fill {
    height: 100%;
    transition:
      width,
      background-color;
  }

  img {
    margin-left: 145px;
  }

  .tempText {
    position: absolute;
    width: 100%;
    z-index: 1;
    top: 185px;
    left: 45px;
  }
</style>
