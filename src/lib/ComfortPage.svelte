<script>
  import thermometer from "../assets/Thermometer.webp";
  import sponge from "../assets/FirmnessImages/Sponge.png";
  import ball from "../assets/FirmnessImages/Ball.png";
  import bottle from "../assets/FirmnessImages/Bottle.png";
  import wood from "../assets/FirmnessImages/Wood.avif";
  import steel from "../assets/FirmnessImages/Steel.png";
  import diamond from "../assets/FirmnessImages/Diamond.webp";
  // Declare a reactive variable for progress
  export let setTemperature = 50;
  export let temperature = 50;
  let tempStatus = "No Change";
  export let updateTemperature; // Function to send updates to the parent

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

  // Function to interpolate between colors representing temperature
  $: textColor =
    temperature < 45
      ? // Below 40, keep it Blue (No color change)
        `rgb(0, 0, 0)`
      : temperature < 55
        ? // Interpolate from Blue (0, 0, 255) to Light Blue (0, 255, 255) between 40% and 55%
          `rgb(255, ${255 - Math.round(255 * ((temperature - 40) / 15))}, 0)`
        : temperature < 70
          ? // Interpolate from Light Blue (0, 255, 255) to Yellow (255, 255, 0) between 55% and 70%
            `rgb(${255 - Math.round(255 * ((temperature - 55) / 15))}, 0, ${255 - (255 - Math.round(255 * ((temperature - 55) / 15)))})`
          : temperature < 80
            ? // Interpolate from Yellow (255, 255, 0) to Orange (255, 165, 0) between 70% and 80%
              `rgb(0, ${255 - (255 - Math.round(90 * ((temperature - 70) / 10)))}, 255)`
            : // Interpolate from Orange (255, 165, 0) to Red (255, 0, 0) between 80% and 90%
              temperature <= 90
              ? `rgb(0, ${255 - Math.round(165 - 165 * ((temperature - 80) / 10))}, 255)`
              : // Above 90, keep it Red (No color change)
                `rgb(0, 255, 255)`;

  export let setFirmness = 50;
  export let firmness = 50;
  let firmnessStatus = "No Change";
  export let updateFirmness; // Function to send firmness updates to the parent
  
  $: firmnessImg =
    firmness < 17
      ? sponge
      : firmness < 33
        ? ball
        : firmness < 50
          ? bottle
          : firmness < 67
            ? wood
            : firmness < 83
              ? steel
              : diamond;

  function wait(ms) {
    return new Promise((resolve) => setTimeout(resolve, ms));
  }

  export async function changeTemperature() {
    await wait(5000);
    while (temperature != setTemperature) {
      if (temperature < setTemperature) {
        tempStatus = "Warming Up...";
        temperature += 0.1;
        await wait(10);
      } else if (temperature > setTemperature) {
        tempStatus = "Cooling Down...";
        temperature -= 0.1;
        await wait(10);
      }
      temperature = Number(temperature.toFixed(1));

      // Send the updated temperature to the parent component
      updateTemperature(temperature);
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
      } else if (firmness > setFirmness) {
        firmnessStatus = "Softening...";
        firmness -= 0.1;
        await wait(10);
      }
      firmness = Number(firmness.toFixed(1));

      // Send the updated firmness to the parent component
      updateFirmness(firmness);
    }
    firmnessStatus = "No Change";
  }
</script>



<slot name="comfortMain">
<div class="comfortPage">
  <h1 class="header">Comfort</h1>
  <div class="mainContent">
    <div class="temperature">
      <h1>Temperature</h1>
      <div class="subContent">
        <div class="text">
          <h2>
            Current<br />Pillow<br />Temperature<br /><br />Status: {tempStatus}
          </h2>
        </div>
        <div class="value">
          <img
            class="tempImage"
            alt="Thermometer"
            style="margin-left: 50px !important;"
            src={thermometer}
          />
          <div class="progress-bar">
            <!-- Gradient fill that dynamically changes width and color -->
            <div
              class="fill"
              style="width: {(temperature - 40) *
                2}%; background-color: {temperatureColor};"
            ></div>
          </div>
          <h2 class="tempText" style="color: {textColor};">
            {Math.round(temperature)}°
          </h2>
          <!--<progress class="tempProgress" style="--progress-color: {progressColor};" max="100" value={progress}></progress>-->
        </div>
      </div>
      <div class="subContent">
        <div class="text">
          <h2>Set<br />Pillow<br />Temperature</h2>
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
          <h2>
            Current<br />Pillow<br />Firmness<br /><br />Status: {firmnessStatus}
          </h2>
        </div>
        <div class="value">
          <h1>{Math.round(firmness)}%</h1>
          <img
            style="margin-left: 25% !important;"
            alt="Pillow Firmness"
            width="100px"
            height="auto"
            src={firmnessImg}
          />
        </div>
      </div>
      <div class="subContent">
        <div class="text">
          <h2>Set<br />Pillow<br />Firmness</h2>
        </div>
        <div class="value">
          <div class="progress-container">
            <!-- Range Slider to edit progress -->
            <input
              type="range"
              min="0"
              max="100"
              bind:value={setFirmness}
              on:change={changeFirmness}
            />

            <!-- Display the percentage -->
            <p>{setFirmness}%</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</slot>


<slot name="temperature" >
  <!-- Default content for temperature if none provided -->
  Temperature: {temperature}°C
  <br>
  Firmness: {firmness}
  <br>
</slot>

<style>
  h1,
  h2 {
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

  input[type="range"] {
    width: 100%;
  }

  .tempImage {
    height: 250px;
    width: auto;
    z-index: 100;
  }

  /* Custom progress bar styling */
  .progress-bar {
    top: 97px;
    left: -28px;
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
    transition: width, background-color;
  }

  .tempText {
    position: absolute;
    width: 50px;
    z-index: 1;
    top: 185px;
    left: 64px;
  }
</style>
