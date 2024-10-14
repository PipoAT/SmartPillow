<script>
  let activeSection = null;
  import Settings from './Pillow_Settings.svelte'; 

  function handleSectionClick(section) {
    activeSection = activeSection == section ? null : section;
  }

  let sectionNames = ["Sleep & Health", "Alarm", "Comfort", "Personalization", "Settings"];
</script>

<!-- UI Region -->
<div class="container"> 
  <div class="ui-region">
    <div class="title-bar"><p>UI Region</p></div>
    <div> 
      {#each sectionNames as section}
      <!-- svelte-ignore a11y-no-static-element-interactions -->
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <div
        class="section {activeSection == section ? 'expanded' : ''}"
        on:click={() => handleSectionClick(section)}
      >
        <div class="content-placeholder">{section}</div>
        <div class="content" on:click|stopPropagation>
          {#if activeSection === section}
            {#if section == "Sleep & Health"}
              <p>import "Sleep & Health" container here</p>
            {/if}
            {#if section == "Settings"}
              <Settings />
            {/if}
          {/if}
        </div>
      </div>
    {/each}
    </div>
  </div>

  <!-- ---------------Testing UI ------------------>
  <div class="testing-info-region">
    <div class="title-bar">
      <p>Testing UI Partition</p>
    </div>
    <p>testing info</p>
  </div>
</div>
