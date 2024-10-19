<script>
  let connectToPhone = false;
  let timeFormat = "24hr";
  let defaultVolume = 50;
  let profileInfo = {
    name: "Kate Plas",
    email: "kate@gmail.com"
  };

  function returnToDefault() {
    connectToPhone = false;
    timeFormat = "24hr";
    defaultVolume = 50;
  }
</script>


  <h2>Settings</h2>

  <div class="setting-item">
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label>Connect to Phone</label>
    <input type="checkbox" bind:checked={connectToPhone} />
  </div>

  <div class="setting-item">
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label>Time Format</label>
    <select bind:value={timeFormat}>
      <option value="24hr">24 Hour</option>
      <option value="12hr">12 Hour</option>
    </select>
  </div>

  <div class="setting-item">
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label>Default Volume</label>
    <input type="range" min="0" max="100" bind:value={defaultVolume} />
    <span>{defaultVolume}%</span>
  </div>

  <div class="setting-item">
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label>Profile Info</label>
    <div class="profile-info">
      <p>Name: {profileInfo.name}</p>
      <p>Email: {profileInfo.email}</p>
    </div>
  </div>

  <button on:click={returnToDefault} class="reset-button">Return to Default</button>


<style>


  h2 {
    /** text-align: center; **/
    margin-bottom: 20px;
  }

  .setting-item {
    margin-bottom: 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .setting-item label {
    font-weight: bold;
  }

  .setting-item input[type="range"] {
    width: 150px;
  }

  .profile-info p {
    margin: 5px 0;
  }

  .reset-button {
    display: block;
    width: 100%;
    padding: 10px;
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    text-align: center;
  }

  .reset-button:hover {
    background-color: #0056b3;
  }
</style>
