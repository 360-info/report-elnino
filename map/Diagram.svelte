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
  let activeButton;
  let diagramTitle = "El Niño impacts explained";
  let diagramSubtitle = "James Goldie & Michael Joiner, 360info";
  
  // handler: update title block state based on info from the pushed button 
  function updateTitleBlock(e) {
    activeButton = e.detail.id;
    diagramTitle = e.detail.title;
    diagramSubtitle = e.detail.description;
  }

  // returns true if an active button id is defined but not the supplied id
  function activeButtonIsNot(x) {
    activeButton !== undefined && activeButton != x
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
    sizeClass == "x-large" ? 60 : 
    sizeClass == "large" ? 40 :
    sizeClass == "medium" ? 30 :
    20;

</script>

<svelte:window bind:innerWidth />

<div class="mapstack" style:aspect-ratio="{diagramAspectRatio}">
  <MapBG/>
  <MapSSTs/>
  <MapLandGrid/>
  <MapWalkerCirc/>
  <!-- India -->
  <Button
    icon="fa6-solid:sun-plant-wilt"
    top="33%" left="33%" color="#994000"
    size={buttonSize}
    buttonID="india-drought"
    title="Drought in India"
    description="Here're some facts about that..."
    on:buttonActivate={updateTitleBlock}
    deemphasised={
      activeButton !== undefined &&
      activeButton != "india-drought"}
     />
  <!-- SE Asia -->
  <Button
    icon="wi:day-haze"
    top="39%" left="40%" color="#b59d8c" iconScale=0.8
    size={buttonSize}
    buttonID="seasia-haze"
    title="Haze in SE Asia"
    description="Here're some other facts about haze. Fugiat aute mollit sunt do excepteur deserunt. Et et ipsum amet quis cupidatat do deserunt deserunt laboris esse."
    on:buttonActivate={updateTitleBlock}
    deemphasised={
      activeButton !== undefined &&
      activeButton != "seasia-haze"}
    />
  <!-- SE Aus -->
  <Button
    icon="fa6-solid:fire"
    top="51%" left="51%" color="#ff4600"
    size={buttonSize}
    buttonID="fire-seaus"
    title="Fire in SE Australia"
    description="Here're some other facts about fire. Eu aliqua nostrud fugiat cillum. In elit cupidatat sunt anim cupidatat nulla dolore. Reprehenderit eu dolor culpa ad. Mollit amet eu et ad dolore."
    on:buttonActivate={updateTitleBlock}
    deemphasised={
      activeButton !== undefined &&
      activeButton != "fire-seaus"}
    />
  <Button
    icon="fa6-solid:sun-plant-wilt"
    top="56%" left="48%" color="#994000"
    size={buttonSize}
    buttonID="drought-seaus"
    title="Drought in SE Australia"
    description="Drought is interesting for several reasons! Aute enim cillum irure reprehenderit tempor commodo nostrud laboris."
    on:buttonActivate={updateTitleBlock}
    deemphasised={
      activeButton !== undefined &&
      activeButton != "drought-seaus"}
    />
  <!-- Pacific -->
  <Button
    icon="fa6-solid:sun-plant-wilt"
    top="45%" left="56%" color="#994000"
    size={buttonSize}
    buttonID="drought-spac"
    title="Drought in the south Pacific"
    description="Drought is interesting for several reasons! it could be different in the Pacific, though, where water storages are incredibly important."
    on:buttonActivate={updateTitleBlock}
    deemphasised={
      activeButton !== undefined &&
      activeButton != "drought-spac"}
    />
  <Button
    icon="fa6-solid:hurricane"
    top="45%" left="70%" color="#0095d0" iconScale=0.5
    size={buttonSize}
    buttonID="hurricane-pac"
    title="Hurricanes in the Pacific"
    description="Parts of the Pacific that sit near the zone of shifted convection often have to deal with more hurricanes than average during El Niños."
    on:buttonActivate={updateTitleBlock}
    deemphasised={
      activeButton !== undefined &&
      activeButton != "hurricane-pac"}
    />
  <!-- Nth. America -->
  <Button
    icon="fa6-solid:house-flood-water"
    top="22%" left="72%" color="#005bd0"
    size={buttonSize}
    buttonID="flood-seusa"
    diagramTitle = "Extreme rain in the south-eastern US"
    description="Extreme rainfall can be debilitating, risking homes and lives in flooding. Minim officia proident anim aliqua."
    on:buttonActivate={updateTitleBlock}
    deemphasised={
      activeButton !== undefined &&
      activeButton != "flood-seusa"}
    />
  <Button
    icon="fa6-solid:hurricane"
    top="25%" left="86%" color="#0095d0" iconScale=0.5
    size={buttonSize}
    buttonID="hurricane-alt"
    diagramTitle = "Hurricanes in the Atlantic"
    description="The Atlantic Ocean often sees quieter hurricane seasons during El Niños, with fewer hurricanes than in a typical year. The ocean is so hot this year, however, that US authorities are forecasting an average hurricane season."
    on:buttonActivate={updateTitleBlock}
    deemphasised={
      activeButton !== undefined &&
      activeButton != "hurricane-alt"}
    />
</div>

<!-- title block -->

<div id="map-description">
  {#key diagramTitle}
  <h2
    in:fly={{ y: 20, duration: 200, delay: 200 }}
    out:fly={{ y: 20, duration: 200 }}
    id="map-description-title"
    class="title-{sizeClass}"
    >
    {diagramTitle}
  </h2>
  {/key}
  {#key diagramSubtitle}
  <p
    in:fly={{ y: 20, duration: 200, delay: 200 }}
    out:fly={{ y: 20, duration: 200 }}
    id="map-description-desc">
    {diagramSubtitle}
  </p>
  {/key}
</div>

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

  /* animate walker circulation lines */

  @media (prefers-reduced-motion: no-preference) {
    @keyframes walkerascension {
      0% { stroke-dashoffset: 0; }  
      100% { stroke-dashoffset: -6px; }
    }
    #elnino-walker-ascend {
      animation: 0.3s linear 0s infinite walkerascension;
    }
    
    @keyframes walkersidesdescend {
      0% { stroke-dashoffset: 0; }  
      100% { stroke-dashoffset: -13px; }
    }
    #elnino-walker-sidesdescend {
      animation: 2.5s linear 0s infinite walkersidesdescend;
    }
  }
</style>
