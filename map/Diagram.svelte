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
     top="10%" left="53.5%" color="#dd0000"
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
      description="After three years of La Niña, drought in Somalia is the worst it’s been in decades — described as <a href='https://public.wmo.int/en/media/news/climate-change-made-horn-of-africa-drought-and-mediterranean-heat-%E2%80%9C100-times-more-likely%E2%80%9D'>“100 times more likely”</a> because of climate change by the World Meteorological Organization.<br><br>An El Niño could provide relief — but extreme, flooding rains are also possible, which may be little relief at all."
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
      description="Every year around June, the winds around India change, bringing rain from the Indian Ocean. This monsoon rainfall is critical to many of India’s <em>kharif</em> crops, which grow at this time of year.<br><br>El Niño often disrupts the timing or intensity of the monsoon, making rainfall scarcer and less predictable."
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
      description="Fires from land clearing and other activities cause a smokey haze to drift across countries in Southeast Asia. El Niño can exacerbate the haze by making the land drier and more fire-prone, as the altered winds move rainfall away from Asia.<br><br>The airborne pollutants from smoke haze can cause respiratory disease, and El Niño often brings other temperature-related impacts, like increases in heat stroke and vector-borne diseases like malaria and dengue."
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
      description="Southeastern Australia is often drier and warmer during an El Niño. This is a problem for farmers, who rely on steady rainfall for growth."
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
      description="Southeastern Australia is often drier and warmer during an El Niño. This elevates fire risk in the Australian summer, as drier vegetation is more likely to catch fire and is harder to put out in hotter or windier conditions."
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
      title="Tropical cyclones ↓ in nth Australia"
      description="On average, tropical cyclones (called <em>typhoons</em> or <em>hurricanes</em> elsewhere) tend to be less frequent near Australia during an El Niño."
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
      description="Like south-eastern Australia, Pacific Islands often <a href='https://doi.org/10.1007/s10584-021-03112-1'>get less rainfall</a> during an El Niño, contributing to drought conditions.<br><br>Droughts often mean residents need to travel further to find water, or even hire trucks to deliver it from elsewhere. Food security is also impacted — and some islands with mountainous regions can be impacted by frosts at the same time.
      "
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
      title="Hurricanes ↑ in east Pacific"
      description="The eastern and central Pacific tend to see more hurricanes during an El Niño, as warmer waters are the fuel that sustains a hurricane."
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
      diagramTitle = "Extreme rain in SW USA"
      description="Jet streams are fast streams of air that wrap around the Earth, high up in the atmosphere. El Niño diverts the subtropical northern hemisphere jet over the southwestern US, where it often brings extreme rainfall and flooding to states like California."
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
      diagramTitle = "Hurricanes ↓ in nth Atlantic"
      description="On average, hurricanes (called <em>typhoons</em> or <em>tropical cyclones</em> elsewhere) tend to be less frequent in the North Atlantic Ocean during an El Niño.<br><br>However, this year NOAA has forecast an average hurricane season despite the El Niño. This is because the North Atlantic is very warm, promoting hurricane activity."
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
      description="El Niño was <a href='https://earthobservatory.nasa.gov/features/ElNino/page3.php'>named hundreds of years ago by Peruvian fishers</a>, who noticed a change in the currents that would bring hot water and a smaller catch.<br><br>El Niño continues to impact catches and change the species available to fisheries off the coast of South America."
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
    {diagramTitle || "El Niño impacts"}
  </h2>
  {/key}
  {#key diagramSubtitle}
  <p
    in:fly={{ y: 20, duration: 200, delay: 200 }}
    out:fly={{ y: 20, duration: 200 }}
    class="description-{sizeClass}">
    {@html diagramSubtitle || "James Goldie & Michael Joiner, 360info"}
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

  #map-description p.description-x-large { font-size: 120%; }
  #map-description p.description-large   { font-size: 100%; }
  #map-description p.description-medium  { font-size: 80%; }
  #map-description p.description-small   { font-size: 70%; }

</style>
