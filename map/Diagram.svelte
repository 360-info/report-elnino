<script>
  import {selectAll, attr, classed} from "d3-select"
  import Map from "./Map.svelte"

  // TODO - add interaction handlers and classes programmatically
  let svg = d3.select("#map")
  let allButtons = selectAll("[id^=\"btn-\"]");
  allButtons
    .attr("tabindex", "0")
    .classed("impactbtn", true)
    // .on("click", updateImpactState);

</script>

<div id="map-description">
  <h2 id="map-description-title">El Niño impacts</h2>
  <p id="map-description-desc">James Goldie & Michael Joiner, 360info</p>
</div>

<Map />

<style>
  @import url('https://fonts.googleapis.com/css2?family=Public+Sans:wght@300;700;900&display=swap');

  :global(svg) {
		max-width: 100%;
		display: block
	}

  .impactbtn {
    transition: all 0.3s ease-out;
    transform-origin: center;
    transform-box: fill-box;
  }

  .impactbtn:hover,
  .impactbtn:focus
  {
    transform: scale(1.5);
    filter: brightness(110%) drop-shadow(3px 3px 5px #00000033);
    outline: none;
  }

  /* make the button pulse when it's the selected one (unless reduced motion) */

  @keyframes btnpulse {
    0% {
      transform: scale(1);
      opacity: 100%;
    }  
    100% {
      transform: scale(2.5);
      opacity: 0%;
    }
  }

  .impactbtn.activebtn g[id$="btnpulse"] {
    animation: 1.5s linear 0s infinite btnpulse;
    transform-origin: center;
    transform-box: fill-box;
    /* transform: scale(1.75); */
  }

  @media (prefers-reduced-motion) {
    .impactbtn.activebtn g[id$="btnpulse"] {
      animation: none;
      transform: scale(1.75);
    }
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
