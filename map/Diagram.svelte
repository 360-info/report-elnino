<script>
  import { fly } from "svelte/transition";
  import Button from "./Layers/Button.svelte";
  import MapBG from "./Layers/MapBG.svelte";
  import MapLandGrid from "./Layers/MapLandGrid.svelte";
  import MapSSTs from "./Layers/MapSSTs.svelte";
  import MapWalkerCirc from "./Layers/MapWalkerCirc.svelte";

  // from svg layer viewBoxes. fixes icon % positioning 
  let diagramBoxWidth = 1098.37;
  let diagramBoxHeight = 444.18;
  let diagramAspectRatio = diagramBoxWidth + " / " + diagramBoxHeight;

  // diagram state received from buttons' `buttonActivate` messages
  let activeButton = "none";
  let diagramTitle = "El Niño: global impacts";
  let diagramSubtitle = "James Goldie & Michael Joiner, 360info";

  // timer ids (to reset if we hit another button)
  let stage1Timer;
  let stage2Timer;
  
  // handler: update title block state based on info from the pushed button 
  function updateTitleBlock(e) {
    console.log("Title update received. Clearing timers...")
    // clear any active timer on "how it works" below (no stress if not defined)
    clearTimeout(stage1Timer);
    clearTimeout(stage2Timer);

    // update active button and title block
    activeButton = e.detail.id;
    diagramTitle = e.detail.title;
    diagramSubtitle = e.detail.description;
  }

  // when the map is clicked, cancel and return to the default state
  function returnToDefault() {
    console.log("Returning to default...")
    updateTitleBlock({
      detail: {
        id: "none",
        title: undefined,
        subtitle: undefined
      }
    });
  }

  // handler for "how it works button": start first stage, start other stages
  // on timer
  function runHowItWorks() {
    activeButton = "walker-circulation-start";
    diagramTitle = "How El Niño works";
    diagramSubtitle = " ";

    // other stages on timer
    stage1Timer = setTimeout(() => {
      activeButton = "walker-circulation-mid";
    }, 10000);
    stage2Timer = setTimeout(() => {
      activeButton = "none";
      diagramTitle = undefined;
      diagramSubtitle = undefined;
    }, 20000);
  }

  // TODO - add aria attributes

  // track window width to shrink components for mobile
  let innerWidth;
  let sizeClass;
  let buttonSize;
  $: sizeClass =
    innerWidth >= 1200 ? "x-large" : 
    innerWidth >= 992 ? "large" :
    innerWidth >= 768 ? "medium" :
    "small";
  $: buttonSize =
    sizeClass == "x-large" ? 45 : 
    sizeClass == "large" ? 40 :
    sizeClass == "medium" ? 30 :
    20;

</script>

<svelte:window bind:innerWidth />

<div class="mapstack" style:aspect-ratio="{diagramAspectRatio}">
  <MapBG />
  <MapSSTs
    layerState={
      activeButton == "walker-circulation-mid" ?
        "shown" :
        activeButton == "walker-circulation-end" ?
          "deemphasised" :
          "hidden"
    }
  />
  <MapLandGrid
    on:mapClicked={returnToDefault}
  />
  <!-- how it works: walker circulation can either be:
    - "walker-circulation-start" (when button is hit),
    -  "walker-circulation-mid" (after a few seconds),
    -  ""walker-circulation-end" (after mid is finished) -->
  <MapWalkerCirc
    on:mapClicked={returnToDefault}
    layerState={
      activeButton == "walker-circulation-start" ?
        "start" :
        activeButton == "walker-circulation-mid" ?
          "mid" :
          activeButton == "walker-circulation-end" ?
          "end" :
          "hidden"
    }
  />
  <Button
    icon="ph:question-fill"
    top="14.25%" left="50.25%" color="#fc8c03"
    size={buttonSize * 1.25}
    borderRadius="0"
    title="How El Niño works"
    description=""
    on:buttonActivate={runHowItWorks}
    layerState={
      activeButton.startsWith("walker-circulation-") || activeButton == "none" ?
        "shown" : "deemphasised"
    }
    deemphasised={
      activeButton !== undefined &&
      activeButton != "walker-circulation"}
    />
    <Button
     icon="material-symbols:cancel"
     top="10%" left="55%" color="#dd0000"
     size={buttonSize * 0.8}
     borderRadius="0"
     title="Cancel"
     on:buttonActivate={returnToDefault}
     layerState={
      activeButton.startsWith("walker-circulation-") ? "shown" : "hidden"
      }
    />
  
  <!-- impact buttons -->
  {#if activeButton != "walker-circulation"}
    <!-- Africa -->
    <Button
      icon="wi:day-rain"
      top="30%" left="24%" color="#005bd0"
      size={buttonSize}
      buttonID="africa-rain"
      title="Rain in Eastern Africa"
      description="Here're some facts about that..."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "africa-rain") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <!-- India -->
    <Button
      icon="fa6-solid:sun-plant-wilt"
      top="28%" left="32%" color="#994000"
      size={buttonSize}
      buttonID="india-drought"
      title="Drought in India"
      description="Here're some facts about that..."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "india-drought") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <!-- SE Asia -->
    <Button
      icon="wi:day-haze"
      top="35%" left="38%" color="#b59d8c" iconScale=0.8
      size={buttonSize}
      buttonID="seasia-haze"
      title="Haze in SE Asia"
      description="Here're some other facts about haze. Fugiat aute mollit sunt do excepteur deserunt. Et et ipsum amet quis cupidatat do deserunt deserunt laboris esse."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "seasia-haze") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <!-- Australia -->
    <Button
      icon="fa6-solid:sun-plant-wilt"
      top="52%" left="45%" color="#994000"
      size={buttonSize}
      buttonID="drought-seaus"
      title="Drought in SE Australia"
      description="Drought is interesting for several reasons! Aute enim cillum irure reprehenderit tempor commodo nostrud laboris."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "drought-seaus") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <Button
      icon="fa6-solid:fire"
      top="46%" left="48%" color="#ff4600"
      size={buttonSize}
      buttonID="fire-seaus"
      title="Fire in SE Australia"
      description="Here're some other facts about fire. Eu aliqua nostrud fugiat cillum. In elit cupidatat sunt anim cupidatat nulla dolore. Reprehenderit eu dolor culpa ad. Mollit amet eu et ad dolore."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "fire-seaus") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <Button
      icon="fa6-solid:hurricane"
      top="34%" left="48%" color="#0095d0" iconScale=0.5
      size={buttonSize}
      buttonID="tropcyc-neaus"
      title="Fewer tropical cyclones in northern Australia"
      description="In pariatur officia commodo Lorem enim enim nostrud velit sint dolore labore amet. Ea voluptate Lorem et id et laborum fugiat id eiusmod ad. Irure ea cupidatat voluptate quis. Lorem non velit nulla."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "tropcyc-neaus") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <!-- Pacific -->
    <Button
      icon="fa6-solid:sun-plant-wilt"
      top="41%" left="53%" color="#994000"
      size={buttonSize}
      buttonID="drought-spac"
      title="Drought in the south Pacific"
      description="Drought is interesting for several reasons! it could be different in the Pacific, though, where water storages are incredibly important."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "drought-spac") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <Button
      icon="fa6-solid:hurricane"
      top="32%" left="71%" color="#0095d0" iconScale=0.5
      size={buttonSize}
      buttonID="hurricane-pac"
      title="Hurricanes in the Pacific"
      description="Parts of the Pacific that sit near the zone of shifted convection often have to deal with more hurricanes than average during El Niños."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "hurricane-pac") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <!-- Nth. America -->
    <Button
      icon="fa6-solid:house-flood-water"
      top="18%" left="68%" color="#005bd0"
      size={buttonSize}
      buttonID="flood-seusa"
      diagramTitle = "Extreme rain in the south-eastern US"
      description="Extreme rainfall can be debilitating, risking homes and lives in flooding. Minim officia proident anim aliqua."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "flood-seusa") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <Button
      icon="fa6-solid:hurricane"
      top="15%" left="82%" color="#0095d0" iconScale=0.5
      size={buttonSize}
      buttonID="hurricane-alt"
      diagramTitle = "Hurricanes in the Atlantic"
      description="The Atlantic Ocean often sees quieter hurricane seasons during El Niños, with fewer hurricanes than in a typical year. The ocean is so hot this year, however, that US authorities are forecasting an average hurricane season."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "hurricane-alt") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
      />
    <!-- Sth. America -->
    <Button
      icon="ph:fish-bold"
      top="36%" left="78%" color="#994000" iconScale=0.5
      size={buttonSize}
      buttonID="foodsec-stham"
      diagramTitle = "Food security in Sth America"
      description="Sunt laborum reprehenderit anim aliqua nisi fugiat amet eiusmod consequat aute non ipsum. Esse id cupidatat nisi id aliquip. Exercitation deserunt labore laboris irure voluptate ea voluptate."
      on:buttonActivate={updateTitleBlock}
      layerState={
        (activeButton == "none" || activeButton == "foodsec-stham") ?
          "shown" :
          activeButton.startsWith("walker-circulation-") ?
            "hidden" :
            "deemphasised"
      }
    />
  {/if}
</div>

<!-- title block -->

<output id="map-description">
  {#key diagramTitle}
  <h2
    in:fly={{ y: 20, duration: 200, delay: 200 }}
    out:fly={{ y: 20, duration: 200 }}
    id="map-description-title"
    class="title-{sizeClass}"
    >
    {diagramTitle || "El Niño: global impacts"}
  </h2>
  {/key}
  {#key diagramSubtitle}
  <p
    in:fly={{ y: 20, duration: 200, delay: 200 }}
    out:fly={{ y: 20, duration: 200 }}
    id="map-description-desc">
    {diagramSubtitle || "James Goldie & Michael Joiner, 360info"}
  </p>
  {/key}
</output>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Public+Sans:wght@300;700;900&display=swap');

  /* svg positioning */

  :global(svg) {
		max-width: 100%;
		display: block;
    position: absolute;
	}

  :global(#mapBG),
  :global(#mapSSTs),
  :global(#mapLandGrid),
  :global(#mapWalkerCirc) {
    top: 0;
    left: 0;
  }

  .mapstack {
    max-width: 100%;
    position: relative;
  }

  /* shrink title for mobile */

  #map-description h2.title-x-large { font-size: 300%; }
  #map-description h2.title-large   { font-size: 275%; }
  #map-description h2.title-medium  { font-size: 225%; }
  #map-description h2.title-small   { font-size: 150%; }

</style>
