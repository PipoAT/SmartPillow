<!-- UI Region -->
<div class="basecontainer"> 
  <div class="background-cloud">
  <div class="ui-region">
    <div class="background">
    <div class="title-bar">
      <p>Device UI Partition</p>
    </div>
      
      {#each clouds as cloud}
        <CloudyIcon
          class="cloud"
          style="
            width: {cloud.size}px; 
            height: {cloud.size}px; 
            left: {cloud.x}%; 
            top: {cloud.y}%; 
            transform: scale({cloud.r});
          "
        />
      {/each}
    
      {#each cloudys as cloud}
      <CloudIcon
        class="cloud"
        style="
          width: {cloud.size}px; 
          height: {cloud.size}px; 
          left: {cloud.x}%; 
          top: {cloud.y}%; 
          transform: scale({cloud.r});
        "
      />
      {/each}
    <p class="user-title">Hello, User</p>
    <div class="upcontainer" style:display={showSquares ? 'flex' : 'none'}>
      <div class="square" on:click={() => handleSquareClick('Alarm')}>
        <div class="icon-box-square">
          <AlarmClock />
          <p>Upcoming Alarm: {upcomingAlarm}</p>

        </div>
      </div>
      <div class="square" on:click={() => handleSquareClick('Setting')}>Setting
        
      </div>
      
    </div>
</div>
    <!--  <button class="reset-button" on:click={resetSquares}>Show Squares Again</button>  -->

    <!-- Dropdown Sleep/Health -->
    <div class="dropdown">
      <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown1', event)}>
        <div class="icon-box">
          <BedDouble />
        </div>
        <span class="text">Sleep/Health</span>
      </button>
      <div class="dropdown-content" id="dropdown1">
        <p>This is the hidden information for Dropdown 1.</p>
      </div>
    </div>

    <!-- Dropdown Alarm -->
    <div class="dropdown">
      <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown2', event)}>
        <div class="icon-box">
          <AlarmClock />
        </div>
        <span class="text">Alarm</span>
      </button>
      <div class="dropdown-content" id="dropdown2">
        <div class="container">
          <div class="header">
            <h1>My Alarm Manager</h1>
            <button class="plus-button" on:click={toggleMenu}>+</button>
          </div>

          <div id="alarms-container" class="alarms-container"></div>
          <div id="popup-menu" class="popup-menu">
            <div class="menu-header">
              <button class="menu-button" on:click={() => {stopAudio(); closeMenu();}}>Cancel</button>
              <button class="menu-button" on:click={() => {stopAudio(); saveAndClose();}}>Save</button>
            </div>
            <!-- Clock dropdowns -->
            <div class="clock-container">
              <label for="hours">Hours:</label>
              <select id="hours">
                <!-- Hours 1 to 12 -->
                {#each Array(12) as _, i}
                  <option value={String(i + 1).padStart(2, '0')}>{String(i + 1).padStart(2, '0')}</option>
                {/each}
              </select>

              <label for="minutes">Minutes:</label>
              <select id="minutes">
                <!-- Minutes 00 to 55, every 5 minutes -->
                {#each Array(12) as _, i}
                  <option value={String(i * 5).padStart(2, '0')}>{String(i * 5).padStart(2, '0')}</option>
                {/each}
              </select>

              <label for="ampm">AM/PM:</label>
              <select id="ampm">
                <option value="AM">AM</option>
                <option value="PM">PM</option>
                </select>
                <label for="audio-select">Choose an Alarm Sound:</label>
                <select id="audio-select" bind:value={selectedAudio} on:change={updateAudio}>
                  <option value="/audio1.mp3" selected>Audio 1</option>
                  <option value="/audio2.mp3">Audio 2</option>
                </select>
                <div class="audio-controls">
                  <button on:click={playAudio}>Play</button>
                  <button on:click={stopAudio}>Stop</button>
                </div>
              </div>
              </div>
            </div>
            </div>
          </div>

          <!-- Dropdown Comfort -->
          <div class="dropdown">
            <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown3', event)}>
            <div class="icon-box">
            <ChartCandlestick />
            </div>
            <span class="text">Comfort</span>
            </button>
            <div class="dropdown-content" id="dropdown3">
            <ComfortPage />
            </div>
          </div>

          <!-- Dropdown Personalization -->
          <div class="dropdown">
            <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown4', event)}>
              <div class="icon-box">
              <UserRoundCog />
              </div>
              <span class="text">Personalization</span>
            </button>
            <div class="dropdown-content" id="dropdown4">
            <h2>Audio</h2>
            <label for="audio-select">Choose an audio file:</label>
            <select id="audio-select" bind:value={selectedAudio} on:change={updateAudio}>
              <option value="/audio1.mp3">Audio 1</option>
              <option value="/audio2.mp3">Audio 2</option>
            </select>
            <div class="audio-controls">
              <button on:click={playAudio}>Play</button>
              <button on:click={stopAudio}>Stop</button>
            </div>
            <br>
            <div class="upload-audio">
              <input type="file" accept="audio/*" />
              <button>Upload Audio</button>
            </div>

            <h2>Color</h2>
            <label for="custom-color">Add a custom color:</label>
            <input type="color" id="custom-color" />
            <button on:click={addCustomColor}>Add Color</button>
            <br>
            <br>
            <label for="color-select">Choose a color:</label>
            <select id="color-select" on:change={updatePillowColor}>
              {#each customColors as color}
              <option value={color}>{color}</option>
              {/each}
              <option value="white">White</option>
              <option value="red">Red</option>
              <option value="green">Green</option>
              <option value="blue">Blue</option>
              <option value="black">Black</option>
              <option value="gray">Gray</option>
              <option value="silver">Silver</option>
              <option value="maroon">Maroon</option>
              <option value="purple">Purple</option>
              <option value="fuchsia">Fuchsia</option>
              <option value="lime">Lime</option>
              <option value="olive">Olive</option>
              <option value="yellow">Yellow</option>
              <option value="navy">Navy</option>
              <option value="teal">Teal</option>
              <option value="aqua">Aqua</option>
              <option value="orange">Orange</option>
              <option value="brown">Brown</option>
              <option value="pink">Pink</option>
              <option value="gold">Gold</option>
              <option value="cyan">Cyan</option>
              <option value="magenta">Magenta</option>
            </select>
        <br>
        <br>
        <div class="color-settings">
          <label for="duration">Set Duration (in minutes):</label>
          <input type="number" id="duration" min="1" max="1440" on:change={updatePillowTimer}/>
          <br>
          <br>
        </div>
      </div>
    </div>

    <!-- Dropdown Setting -->
    <div class="dropdown">
      <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown5', event)}>
        <div class="icon-box">
        <Cog />
        </div>
        <span class="text">Setting</span>
      </button>
      <div class="dropdown-content" id="dropdown5">
        <p>This is the hidden information for Dropdown 5.</p>
      </div>
    </div>
  </div>
</div>
  <!-- Testing UI -->
  <div class="testing-info-region">
    <div class="title-bar">
      <p>Testing UI Partition</p>
    </div>
    <button class="button-test">Wake Up</button>
    <button class="button-test">Sleep</button>
    <button class="button-test">Reset</button>
    <div class="pillow" style="position: relative;
    display: inline-block; justify-content: center; align-items: center;">
      <img id="pillowimage" src="/pillow.png" width="200px" height="200px">
      <img id="pillowoverlay" src="/pillowOverlay.png" width="200px" height="200px">
    </div>
    <p id="pillowcolorindicator" style="display: flex; justify-content: center; align-items: center;">Pillow Color: White</p>
    <p id="pillowduration" style="display: flex; justify-content: center; align-items: center;">Duration: 0 minutes</p> 
  </div>
</div>

<script>
import { onMount } from 'svelte';
import ComfortPage from './lib/ComfortPage.svelte';
import { AlarmClock } from 'lucide-svelte';
import { UserRoundCog } from 'lucide-svelte';
import { Cog } from 'lucide-svelte';
import { BedDouble } from 'lucide-svelte';
import { ChartCandlestick } from 'lucide-svelte';
import { Cloud as CloudIcon, Cloudy as CloudyIcon, Moon } from 'lucide-svelte'; // Import both Cloud and Cloudy icons

let upcomingAlarm = '';
let alarms = [{ time: "08:30 AM", enabled: false }];

let showUiRegion = false;
let pillowImage; // Declare pillowImage variable
let showSquares = true; // State to control the visibility of squares
let selectedAudio = 'src/assets/audio1.mp3';
let audio = new Audio();

let dropdowns = [];
let activeDropdown = null;

let customColors = [];

onMount(() => {
    //dropdowns = document.querySelectorAll('.dropdown-content');
    displayAlarms();
    findUpcomingAlarm();
    let frame;

function loop() {
  frame = requestAnimationFrame(loop);

  clouds = clouds.map(cloud => {
    cloud.x -= 0.07 * cloud.r; // Move left
    if (cloud.x < -10) cloud.x = 110; // Reset to the right side when off-screen
    return cloud;
  });

  cloudys = cloudys.map(cloud => {
    cloud.x -= 0.07 * cloud.r; // Move left
    if (cloud.x < -10) cloud.x = 110; // Reset to the right side when off-screen
    return cloud;
  });

}

loop();

return () => cancelAnimationFrame(frame);
});

let clouds = new Array(5).fill().map((_, i) => {
		return {
			size: Math.random() * (100 - 50) + 50, // Random size between 50px and 100px
			x: 100 + Math.random() * 20, // Start off-screen right
			y: Math.random() * 50, // Random vertical position (0% to 50%)
			r: 0.5 + Math.random() * 1 // Random scale
		};
	});
  let cloudys = new Array(5).fill().map((_, i) => {
		return {
			size: Math.random() * (100 - 50) + 50, // Random size between 50px and 100px
			x: 100 + Math.random() * 20, // Start off-screen right
			y: Math.random() * 50, // Random vertical position (0% to 50%)
			r: 0.5 + Math.random() * 1 // Random scale
		};
	});

	let moonPosition = { x: Math.random() * 100, y: Math.random() * 10 }; // Position for the moon


function findUpcomingAlarm() {
  const currentTime = new Date();
  
  // Convert current time to a comparable format
  const currentHours = currentTime.getHours();
  const currentMinutes = currentTime.getMinutes();

  let closestAlarm = null;
  let closestTimeDiff = Infinity; // To find the minimum time difference
  alarms.forEach(alarm => {
    const [alarmTime, period] = alarm.time.split(' ');
    const [hours, minutes] = alarmTime.split(':').map(Number);
    const alarmHours = period === 'PM' && hours !== 12 ? hours + 12 : (period === 'AM' && hours === 12 ? 0 : hours);
    
    const alarmDate = new Date();
    alarmDate.setHours(alarmHours, minutes, 0); // Set alarm time to today's date

    // Calculate time difference in minutes
    const timeDiff = (alarmDate - currentTime) / (1000 * 60); // Convert milliseconds to minutes

    // Check if the alarm is in the future and closer than the previous closest
    if (timeDiff > 0 && timeDiff < closestTimeDiff) {
      closestTimeDiff = timeDiff;
      closestAlarm = alarm.time;
    }
  });
  console.log(`Action for ${upcomingAlarm} executed`);
  upcomingAlarm = closestAlarm ? closestAlarm : 'No upcoming alarms'; // Fallback if no alarms are found
}

function handleSquareClick(square) {
    showUiRegion = true;
    //showSquares = false; // Hide squares when one is clicked
    handleSquareAction(square);
}

function handleSquareAction(square) {
    // Placeholder for additional actions for each square
    if (square === 'Setting') {

    // Use setTimeout to ensure the dropdown has time to open before scrolling
    setTimeout(() => {
      const dropdown5Element = document.getElementById('dropdown5'); // Ensure this ID is correct
      if (dropdown5Element) {
        dropdown5Element.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    }, 100); // Adjust timeout duration if necessary
    // Toggle dropdown for square 5
    toggleDropdown('dropdown5');
    console.log(`Action for ${square} executed`); // Replace this with your logic

  } else if (square === 'Person') {

    // Use setTimeout to ensure the dropdown has time to open before scrolling
    setTimeout(() => {
      const dropdown4Element = document.getElementById('dropdown4'); // Ensure this ID is correct
      if (dropdown4Element) {
        dropdown4Element.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    }, 100); // Adjust timeout duration if necessary
    // Toggle dropdown for square 4
    toggleDropdown('dropdown4');
    console.log(`Action for ${square} executed`); // Replace this with your logic

  } else if (square === 'Comfort') {

    // Use setTimeout to ensure the dropdown has time to open before scrolling
    setTimeout(() => {
      const dropdown3Element = document.getElementById('dropdown3'); // Ensure this ID is correct
      if (dropdown3Element) {
        dropdown3Element.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    }, 100); // Adjust timeout duration if necessary
    // Toggle dropdown for square 3
    toggleDropdown('dropdown3');
    console.log(`Action for ${square} executed`); // Replace this with your logic

  } else if (square === 'Health') {

    // Use setTimeout to ensure the dropdown has time to open before scrolling
    setTimeout(() => {
      const dropdown2Element = document.getElementById('dropdown1'); // Ensure this ID is correct
      if (dropdown2Element) {
        dropdown2Element.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    }, 100); // Adjust timeout duration if necessary
    // Toggle dropdown for square 2
    toggleDropdown('dropdown1');
    console.log(`Action for ${square} executed`); // Replace this with your logic

  } else if (square === 'Alarm') {

    // Use setTimeout to ensure the dropdown has time to open before scrolling
    setTimeout(() => {
      const dropdown1Element = document.getElementById('dropdown2'); // Ensure this ID is correct
      if (dropdown1Element) {
        dropdown1Element.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    }, 100); // Adjust timeout duration if necessary
    // Toggle dropdown for square 1
    toggleDropdown('dropdown2');
    console.log(`Action for ${square} executed`); // Replace this with your logic
  }
}

function toggleDropdown(dropdownId, event) {
    // Get the main container or body where the blur will be applied
    const mainContainer = document.querySelector('.upcontainer'); // Adjust the selector based on your layout
    const dropdowns = document.querySelectorAll('.dropdown'); // Ensure to select all dropdowns

    dropdowns.forEach(dropdown => {
        if (dropdown.id !== dropdownId) {
            dropdown.previousElementSibling.classList.remove('active'); // Remove active class
        }
      
    });

    const dropdown = document.getElementById(dropdownId);
    if (dropdown.style.display === 'block') {
        dropdown.style.display = 'none';
        event.target.classList.remove('active'); // Remove active class
        mainContainer.classList.remove('blur'); // Remove blur when closing
    } else {
        dropdown.style.display = 'block';
        event.target.classList.add('active'); // Add active class
        mainContainer.classList.add('blur'); // Add blur when opening
    }
}

function toggleMenu() {
    const popupMenu = document.getElementById('popup-menu');
    popupMenu.classList.toggle('show'); // Toggle visibility of the popup
}

function closeMenu() {
    const popupMenu = document.getElementById('popup-menu');
    popupMenu.classList.remove('show'); // Close the popup menu
    var menu = document.getElementById("popup-menu");
    menu.classList.remove("show");
}

function updatePillowColor(event) {
    const selectedColor = event.target.value;
    const pillowImage = document.getElementById('pillowoverlay');
    const canvas = document.createElement('canvas');
    const ctx = canvas.getContext('2d');

    ctx.fillStyle = selectedColor;
    ctx.fillRect(0, 0, 1, 1);

    const pixelData = ctx.getImageData(0, 0, 1, 1).data;
    if (pillowImage) {
      pillowImage.style.backgroundColor = `rgba(${pixelData[0]}, ${pixelData[1]}, ${pixelData[2]}, 0.25)`;
    }

    const textDisplay = document.getElementById('pillowcolorindicator');
    if (textDisplay) {
      textDisplay.innerText = `Pillow color: ${selectedColor}`;
    }
}

function updatePillowTimer(event) {
    const duration = event.target.value;
    const textDisplay = document.getElementById('pillowduration');
    if (textDisplay) {
      textDisplay.innerText = `Duration: ${duration} minutes`;
    }
}

function saveAndClose() {
  // Get selected values
  var hours = document.getElementById("hours").value;
  var minutes = document.getElementById("minutes").value;
  var ampm = document.getElementById("ampm").value;
  
  // Format selected time
  var selectedTime = hours + ":" + minutes + " " + ampm;
  
  // Check for duplicate alarms
  let alarmExists = alarms.some(alarm => alarm.time === selectedTime);
  
  if (alarmExists) {
    // Shake the popup menu
    document.querySelector('.ui-region .popup-menu').classList.add('shake');
    
    // Remove the shake class after animation duration
    setTimeout(() => {
      document.querySelector('.ui-region .popup-menu').classList.remove('shake');
    }, 1250); // Adjust time to match the shake animation duration
    playErrorAudio();
  } else {
    // Check if we can add more alarms
    if (alarms.length < 10) {
      alarms.push({ time: selectedTime, disabled: false });
      displayAlarms();
      closeMenu(); // Close the pop-up menu
    } else {
      alert("Maximum of 10 alarms reached!");
    }
  }
}

function displayAlarms() {
  const alarmsContainer = document.getElementById("alarms-container");
  alarmsContainer.innerHTML = ""; // Clear previous alarms

  // Sort alarms by time
  alarms.sort((a, b) => {
    const [aHours, aMinutes, aPeriod] = a.time.match(/(\d+):(\d+)\s(AM|PM)/).slice(1);
    const [bHours, bMinutes, bPeriod] = b.time.match(/(\d+):(\d+)\s(AM|PM)/).slice(1);

    const aTime = (parseInt(aHours) % 12) + (aPeriod === "PM" ? 12 : 0) + parseInt(aMinutes) / 60;
    const bTime = (parseInt(bHours) % 12) + (bPeriod === "PM" ? 12 : 0) + parseInt(bMinutes) / 60;

    return aTime - bTime;
  });

  alarms.forEach((alarm, index) => {
    const alarmDiv = document.createElement("div");
    alarmDiv.className = "alarm-item";
    alarmDiv.innerText = alarm.disabled ? `DISABLED: ${alarm.time}` : alarm.time;

    // Button to remove alarm
    const removeButton = document.createElement("button");
    removeButton.innerText = "Remove";
    removeButton.onclick = () => removeAlarm(index);
    alarmDiv.appendChild(removeButton);

    // Toggle switch to disable/enable alarm
    const toggleDiv = document.createElement("label");
    toggleDiv.className = "switch";
    const input = document.createElement("input");
    input.type = "checkbox";
    input.checked = !alarm.disabled; // Check if alarm is enabled
    input.onclick = () => toggleAlarm(index); // Toggle alarm state
    const slider = document.createElement("span");
    slider.className = "slider";
    toggleDiv.appendChild(input);
    toggleDiv.appendChild(slider);
    alarmDiv.appendChild(toggleDiv);

    // Style disabled alarms
    if (alarm.disabled) {
      alarmDiv.style.color = "gray"; // Change text color for disabled alarms
      alarmDiv.style.textDecoration = "line-through"; // Add strikethrough effect
    }

    alarmsContainer.appendChild(alarmDiv);
  });
}


function removeAlarm(index) {
    alarms.splice(index, 1); // Remove alarm from array
    displayAlarms(); // Update displayed alarms
    findUpcomingAlarm();
}

function toggleAlarm(index) {
    alarms[index].disabled = !alarms[index].disabled; // Toggle the disabled state
    displayAlarms(); // Update displayed alarms
}

function playAudio() {
    audio.src = selectedAudio;
    audio.play();
}

function stopAudio() {
    audio.pause();
    audio.currentTime = 0;
}

function updateAudio(event) {
    selectedAudio = event.target.value;
}

function playErrorAudio() {
  var audio = new Audio('error.mp3'); // Path to your error.mp3 file
  audio.play();
}


function addCustomColor() {
    const colorInput = document.getElementById('custom-color');
    const color = colorInput.value;
    if (color && !customColors.includes(color)) {
      customColors = [...customColors, color];
    }
}
</script>
