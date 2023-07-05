<script>
  export let inNeutralState = false;
</script>

<svg
  id="MapWalkerCirc"
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 1098.37 444.18">
  <defs>
    <style>
      .walker-descend {
        stroke-dasharray: 0 0 3 10;
      }
      .walker-descend,
      .cls-2 {
        fill: none;
        stroke: #000;
        stroke-linecap: round;
        stroke-miterlimit: 10;
        stroke-width: 2px;
      }
      .cls-2 {
        stroke-dasharray: 0 0 1 5;
      }
    </style>
  </defs>
  <g id="elnino-walker">

    <!-- new ascend bits here -->
    <g
      id="elnino-walker-ascend-seasia"
      class:inNeutralState>
      <path
        class="walker-ascend" d="m636.62,161.96s24.36,1.69,24.36-20V63.76c0-20-24.36-20-24.36-20" />
      <path
        class="walker-ascend" d="m657.29,161.96s9.34,1.69,9.34-20V63.76c0-20-9.34-20-9.34-20" />
      <path
        class="walker-ascend"
        d="m704.01,161.96s-24.36,1.69-24.36-20c0-21.69,0-58.65,0-78.2s24.36-20,24.36-20" />
      <path
        class="walker-ascend" d="m683.35,161.96s-9.34,1.69-9.34-20,0-58.65,0-78.2,9.34-20,9.34-20" />
    </g>
    <g
      id="elnino-walker-ascend-america"
      class:inNeutralState>
      <path
        class="walker-ascend" d="m779.54,161.96s24.36,1.69,24.36-20V63.76c0-20-24.36-20-24.36-20" />
      <path
        class="walker-ascend" d="m800.21,161.96s9.34,1.69,9.34-20V63.76c0-20-9.34-20-9.34-20" />
      <path
        class="walker-ascend"
        d="m846.93,161.96s-24.36,1.69-24.36-20c0-21.69,0-58.65,0-78.2,0-20,24.36-20,24.36-20" />
      <path
        class="walker-ascend"
        d="m826.27,161.96s-9.34,1.69-9.34-20c0-21.69,0-58.65,0-78.2,0-20,9.34-20,9.34-20" />
    </g>
    <g
      id="elnino-walker-ascend-africa"
      class:inNeutralState>
      <path
        class="walker-ascend" d="m229.03,161.96s24.36,1.69,24.36-20V63.76c0-20-24.36-20-24.36-20" />
      <path
        class="walker-ascend" d="m249.69,161.96s9.34,1.69,9.34-20V63.76c0-20-9.34-20-9.34-20" />
      <path
        class="walker-ascend"
        d="m296.42,161.96s-24.36,1.69-24.36-20c0-21.69,0-58.65,0-78.2,0-20,24.36-20,24.36-20" />
      <path
        class="walker-ascend"
        d="m275.75,161.96s-9.34,1.69-9.34-20c0-21.69,0-58.65,0-78.2,0-20,9.34-20,9.34-20" />
    </g>

    <!-- new sides/descend stuff -->
    <g
      id="elnino-walker-sidesdescend"
      class:inNeutralState>
      <path
        class="walker-descend"
        id="walker-curved-asia-left"
        d={inNeutralState ?
          "m296.42,43.76h12.53s19.71.91,19.71,16.6v82.24s.67,19.36-18.2,19.36c-18.87,0-14.03,0-14.03,0" :
          "m296.42,43.76h177.78s19.71.91,19.71,16.6v82.24s.67,19.36-18.2,19.36c-18.87,0-179.28,0-179.28,0"
        }
        />
      <path
        class="walker-descend"
        id="walker-curved-asia-right"
        d={inNeutralState ?
          "m476.06,43.76h-123.21s-19.71.91-19.71,16.6c0,15.69,0,82.24,0,82.24,0,0-.67,19.36,18.2,19.36,18.87,0,124.71,0,124.71,0" :
          "m641.32,43.76h-123.21s-19.71.91-19.71,16.6c0,15.69,0,82.24,0,82.24,0,0-.67,19.36,18.2,19.36,18.87,0,124.71,0,124.71,0"
          }
        />
      <path
        class="walker-descend"
        id="walker-curved-america-left"
        d={inNeutralState ?
          "m549.18,43.76h278.04s19.71.91,19.71,16.6v82.24s.67,19.36-18.2,19.36h-279.54" :
          "m846.93,43.76h151.5s19.71.91,19.71,16.6c0,15.69,0,82.24,0,82.24,0,0,.67,19.36-18.2,19.36-18.87,0-153,0-153,0"
        }
        />
      <path
        class="walker-descend"
        id="walker-curved-amercia-right"
        d={inNeutralState ?
          "m940.62,43.76h-68.63s-19.71.91-19.71,16.6,0,82.24,0,82.24c0,0-.67,19.36,18.2,19.36,18.87,0,70.13,0,70.13,0" :
          "m229.03,43.76h-123.21s-19.71.91-19.71,16.6c0,15.69,0,82.24,0,82.24,0,0-.67,19.36,18.2,19.36,18.87,0,124.71,0,124.71,0"
        }
        />
      <path
        class="walker-descend"
        id="walker-straight-pacific-bottom"
        d="m779.54,161.96c-18.87,0-76.5,0-76.5,0"
        style:opacity={inNeutralState ? 0 : 1}
        />
      <path
        class="walker-descend"
        id="walker-straight-pacific-top"
        d="m779.54,43.85c-18.87,0-76.5,0-76.5,0"
        style:opacity={inNeutralState ? 0 : 1}
        />
      <path
        class="walker-descend"
        id="walker-straight-europe-bottom"
        d="m228.93,161.96c-18.87,0-145.01,0-145.01,0"
        style:opacity={inNeutralState ? 1 : 0}
        />
      <path
        class="walker-descend"
        id="walker-straight-europe-top"
        d="m228.93,43.85c-18.87,0-145.01,0-145.01,0"
        style:opacity={inNeutralState ? 1 : 0}
        />
    </g>

  </g>
</svg>

<style>

  /* general style */

  .walker-descend {
    stroke-dasharray: 0 0 3 10;
  }
  .walker-descend,
  .walker-ascend {
    fill: none;
    stroke: #000;
    stroke-linecap: round;
    stroke-miterlimit: 10;
    stroke-width: 2px;
  }
  .walker-ascend {
    stroke-dasharray: 0 0 1 5;
  }

  /* animate dashed lines */

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
    #elnino-walker-descend {
      animation: 2.5s linear 0s infinite walkersidesdescend;
    }
  }

  /* animate paths, opacity and transform when switching phases */
  
  /* asia and america ascensions translate */
  #elnino-walker-ascend-seasia,
  #elnino-walker-ascend-america {
    transition: all 1.5s ease-out;
  }
  #elnino-walker-ascend-seasia.inNeutralState {
    transform: translateX(-170px);
  }
  #elnino-walker-ascend-america.inNeutralState {
    transform: translateX(175px);
  }
  
  /* africa doesn't move but fades out the inner paths */
  #elnino-walker-ascend-africa {
    transition: opacity 1.5s linear;
  }
  #elnino-walker-ascend-africa.inNeutralState path:nth-child(2n) {
    opacity: 20%;
  }

  /* non-straight walker descend paths animate on path */
  [id^="walker-curved-"] {
    transition: all 1.5s ease-out;
  }

  /* straight walker descend paths animate on opacity */
  [id^="walker-straight-"] {
    transition: opacity 1.5s linear;
  }

</style>