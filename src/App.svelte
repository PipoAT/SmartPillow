<!-- UI Region -->
<div class = "basecontainer"> 
 
  <div class="ui-region">

    <div class="title-bar">
      <p>Device UI Partition</p>
  </div>
  <p class="user-title">Hello, User</p>
  <div class="upcontainer" style:display={showSquares ? 'flex' : 'none'}>
    <div class="square" on:click={() => handleSquareClick('Square 1')}>Square 1

    </div>
    <div class="square" on:click={() => handleSquareClick('Setting')}>Setting

    </div>

  </div>

  <button class="reset-button" on:click={resetSquares}>Show Squares Again</button>
    <!-- Dropdown Sleep/Health -->
    <div class="dropdown">
      <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown1', event)}>
          <span class="text">Sleep/Health</span>
      </button>
      <div class="dropdown-content" id="dropdown1">
          <p>This is the hidden information for Dropdown 1.</p>
      </div>
    </div>

<!-- Dropdown Alarm -->
<div class="dropdown">
  <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown2', event)}>
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
                  <button class="menu-button" on:click={closeMenu}>Cancel</button>
                  <button class="menu-button" on:click={saveAndClose}>Save</button>
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
              </div>
          </div>
      </div>
  </div>
</div>

<!-- Dropdown Comfort -->
<div class="dropdown">
    <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown3', event)}>
        <span class="text">Comfort</span>
    </button>
    <div class="dropdown-content" id="dropdown3">
        <p>This is the hidden information for Dropdown 3.</p>
    </div>
</div>

<!-- Dropdown Personalization -->
<div class="dropdown">
    <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown4', event)}>
        <span class="text">Personalization</span>
    </button>
    <div class="dropdown-content" id="dropdown4">
        <p>This is the hidden information for Dropdown 4.</p>
    </div>
</div>

<!-- Dropdown Setting -->
<div class="dropdown">
    <button class="dropdown-btn" on:click={(event) => toggleDropdown('dropdown5', event)}>
        <span class="text">Setting</span>
    </button>
    <div class="dropdown-content" id="dropdown5">
        <p>This is the hidden information for Dropdown 5.</p>
    </div>
</div>
</div>



  <!-- Testing UI -->
  <div class="testing-info-region">
    <div class = "title-bar">
      <p> Testing UI Partition</p>
    </div>
    <p> testing info </p>
  </div>

</div>

<script>
    import { onMount } from 'svelte';

  let showUiRegion = false;
  let showSquares = true; // State to control the visibility of squares

  function handleSquareClick(square) {
    showUiRegion = true;
    showSquares = false; // Hide squares when one is clicked
    handleSquareAction(square);
  }

  function handleSquareAction(square) {
    // Placeholder for additional actions for each square
    if (square === 'Setting') {
      // Scroll to the ui-region element
      const uiRegionElement = document.getElementById('ui-region');
      if (uiRegionElement) {
        uiRegionElement.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
      // Toggle dropdown for square 4
      toggleDropdown('dropdown5');
    }
    console.log(`Action for ${square} executed`); // Replace this with your logic
  }

  function resetSquares() {
    showSquares = true; // Show squares again
  }


let dropdowns = [];
let activeDropdown = null;

onMount(() => {
    dropdowns = document.querySelectorAll('.dropdown-content');
});

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

        let alarms = []; // Array to hold alarm times

//        function toggleMenu() {
//            var menu = document.getElementById("popup-menu");
//            menu.classList.toggle("show");
//        }

//        function closeMenu() {
//            var menu = document.getElementById("popup-menu");
//            menu.classList.remove("show");
//        }

        function saveAndClose() {
            // Get selected values
            var hours = document.getElementById("hours").value;
            var minutes = document.getElementById("minutes").value;
            var ampm = document.getElementById("ampm").value;

            // Format selected time
            var selectedTime = hours + ":" + minutes + " " + ampm;

            // Check if we can add more alarms
            if (alarms.length < 10) {
                alarms.push({ time: selectedTime, disabled: false });
                displayAlarms();
            } else {
                alert("Maximum of 10 alarms reached!");
            }

            // Close the pop-up menu
            closeMenu();
        }

        function displayAlarms() {
        const alarmsContainer = document.getElementById("alarms-container");
        alarmsContainer.innerHTML = ""; // Clear previous alarms
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
        }

        function toggleAlarm(index) {
            alarms[index].disabled = !alarms[index].disabled; // Toggle the disabled state
            displayAlarms(); // Update displayed alarms
        }

</script>