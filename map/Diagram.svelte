<script>
  import Button from "./Layers/Button.svelte";
  import MapBG from "./Layers/MapBG.svelte";
  import MapLandGrid from "./Layers/MapLandGrid.svelte";
  import MapSSTs from "./Layers/MapSSTs.svelte";
  import MapWalkerCirc from "./Layers/MapWalkerCirc.svelte";

  // from svg layer viewBoxes. fixes icon % positioning 
  let diagramBoxWidth = 1098.37;
  let diagramBoxHeight = 444.18;
  let diagramAspectRatio = diagramBoxWidth + " / " + diagramBoxHeight;

  // let activeButton = ""
  // function changeActiveButton(to) {
  //   activeButton = to;
  // }
  // add to button: on:click={() => updateActiveButton("XXX")}

  // TODO - add aria attributes

</script>

<div id="map-description">
  <h2 id="map-description-title">El Niño impacts</h2>
  <p id="map-description-desc">James Goldie & Michael Joiner, 360info</p>
</div>

<div class="mapstack" style:aspect-ratio="{diagramAspectRatio}">
  <MapBG/>
  <MapSSTs/>
  <MapLandGrid/>
  <MapWalkerCirc/>
  <!-- India -->
  <Button
    icon="fa6-solid:sun-plant-wilt"
    top="33%" left="33%" color="#994000"/>
  <!-- SE Asia -->
  <Button
    icon="wi:day-haze"
    top="39%" left="40%" color="#b59d8c" iconScale=0.8
    />
  <!-- SE Aus -->
  <Button
    icon="fa6-solid:fire"
    top="51%" left="51%" color="#ff4600"
    deemphasised />
  <Button
    icon="fa6-solid:sun-plant-wilt"
    top="56%" left="48%" color="#994000"/>
  <!-- Pacific -->
  <Button
    icon="fa6-solid:sun-plant-wilt"
    top="45%" left="56%" color="#994000"/>
  <Button
    icon="fa6-solid:hurricane"
    top="45%" left="70%" color="#0095d0" iconScale=0.5/>
  <!-- Nth. America -->
  <Button
    icon="fa6-solid:house-flood-water"
    top="22%" left="72%" color="#005bd0"/>
  <Button
    icon="fa6-solid:hurricane"
    top="25%" left="86%" color="#0095d0" iconScale=0.5/>
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
