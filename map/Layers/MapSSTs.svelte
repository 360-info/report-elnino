<script>
  import { fade } from "svelte/transition";

  // state: shown, deemphasised, hidden
  export let layerState;
</script>

{#if layerState != "hidden"}
<svg
  id="MapSSTs"
  class:deemphasised={layerState == "deemphasised"}
  transition:fade={{ duration: 1000 }}
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 1098.37 444.18"
  ><defs
    ><style>
      .sst-cool {
        fill: #1760ff;
      }
      .sst-cool,
      .sst-warm {
        opacity: 0.75;
      }
      .sst-warm {
        fill: #ff3217;
      }
    </style></defs
  ><g id="elnino-ssts"
    ><path
      class="sst-warm"
      d="m937.52,152.62c-11.72-5.85-24.89-8.16-37.95-7.11-24.94,2.01-42.78.62-83.33.41-50.15-.26-142.24,7.85-142.24,26.09s87.83,17.58,154.77,22.79c58.08,4.52,37.61,5.64,94.87,12.96,43.62,5.58,34.8-23.51,29.69-40.12-1.99-6.46-8.54-11.4-15.81-15.03Z"
    /><path
      class="sst-cool"
      d="m538.37,150.63c-14.93-4.73-30.75-5.94-46.21-3.44-19.4,3.13-43.07,10.13-48.24,25.71-9.08,27.34,75.99,36.49,75.99,36.49,0,0,45.61,9.14,58.35,8.21,21.83-1.61,30.86.21,41.03-8.21,9.47-7.84.09-25.29-10.94-31-20.09-10.41-45.56-20.03-69.98-27.76Z"
    />
  </g>
</svg>
{/if}

<style>
  .deemphasised {
    opacity: 0.2;
  }
</style>