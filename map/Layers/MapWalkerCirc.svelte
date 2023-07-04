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
    <g
      id="elnino-walker-ascend"
      class:inNeutralState>
      <path
        class="walker-ascend"
        d="m636.62,181.79s24.36,1.69,24.36-20v-78.2c0-20-24.36-20-24.36-20"
      />
      <path
        class="walker-ascend"
        d="m657.29,181.79s9.34,1.69,9.34-20v-78.2c0-20-9.34-20-9.34-20"
      />
      <path
        class="walker-ascend"
        d="m704.01,181.79s-24.36,1.69-24.36-20c0-21.69,0-58.65,0-78.2s24.36-20,24.36-20"
      />
      <path
        class="walker-ascend"
        d="m683.35,181.79s-9.34,1.69-9.34-20,0-58.65,0-78.2,9.34-20,9.34-20"
      />
    </g>
    <g
      id="elnino-walker-descend"
      class:inNeutralState>
      <path
        class="walker-descend-right"
        d="m704.01,63.59h123.21s19.71.91,19.71,16.6v82.24s.67,19.36-18.2,19.36h-124.71"
      />
      <path
        class="walker-descend-left"
        d="m641.32,63.59h-123.21s-19.71.91-19.71,16.6c0,15.69,0,82.24,0,82.24,0,0-.67,19.36,18.2,19.36,18.87,0,124.71,0,124.71,0"
      />
    </g>
  </g>
</svg>

<style>

  /* general style */
  .walker-descend-left,
  .walker-descend-right {
    stroke-dasharray: 0 0 3 10;
  }
  .walker-descend-left,
  .walker-descend-right,
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

  /* animation when switching phases */

  #elnino-walker-ascend {
    transition: all 1.5s ease-out;
  }

  #elnino-walker-ascend.inNeutralState {
    transform: translate(-170px, 0px);
  }

  #elnino-walker-descend .walker-descend-left {
    transform-box: fill-box;
    transform-origin: left;
    transition:
      opacity 1.5s linear,
      transform 1.5s ease-out;
  }

  #elnino-walker-descend.inNeutralState .walker-descend-left {
    opacity: 0;
    transform: scaleX(0%);
  }

  #elnino-walker-descend .walker-descend-right {
    transform-box: fill-box;
    transform-origin: right;
    transition:
      opacity 1.5s linear,
      transform 1.5s ease-out;
  }

  #elnino-walker-descend.inNeutralState .walker-descend-right{
    transform: scaleX(2.15);
    
  }

</style>