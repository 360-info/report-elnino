<script>
  import { createEventDispatcher } from "svelte";
  import Icon from "@iconify/svelte";

  export let tabindex = "0";
  export let icon;
  export let size = 40;
  export let top;
  export let left;
  export let color = "#666666";
  export let iconScale = 0.6;

  // export let deemphasised = false;
  // export let borderRadius = "50%";

  // id, title and description passed back to global state on click
  export let buttonID;
  export let title = "";
  export let description = "";

  // state: compare active button to this one
  // - "shown", if activeButton matches x or is undefined
  // - "deemphasised", if activeButton is a walker circulation start or mid
  // - "hidden", if activebutton otherwise doesn't match x
  export let layerState;

  /* event handlers: pass the id, title and desc props back on button push */

	const dispatch = createEventDispatcher();
	function activateButton() {
		dispatch("buttonActivate", {
      id: buttonID,
      title: title,
      description: description
		});
	}

  // wrapper handler for activateButton when Enter or space key is pressed
  function onKeyUp(e) {
    if (e.key == "Enter" || e.key == " ") {
      activateButton()
    }
  }
  

</script>


{#if layerState != "hidden"}
  <div
    on:click={activateButton}
    on:keyup={onKeyUp}
    role="button"
    aria-label={title}
    aria-description={description}
    tabindex={tabindex}
    class="mapbutton"
    style:height={size + "px"}
    style:width={size + "px"}
    style:top={top}
    style:left={left}
    style:position="absolute"
    style:background-color={color}
    style:border-radius="50%"
    style:padding-block="5px"
    style:display="flex"
    style:justify-content="center"
    style:align-items="center"
    style:text-align="center"
    style:border="20px solid transparent"
    style:background-clip="content-box"
    style:filter="drop-shadow(0px 0px {size * 0.4}px {color}) {
      layerState == "deemphasised" ? "grayscale(50%) opacity(25%)" : ""}"
    >
    <div
      style:display="flex"
      style:flex-flow="row nowrap"
      style:justify-content="center"
      style:align-items="center"
      style:align-content="center"
      >
      <Icon
        icon={icon}
        width={size * iconScale}  
        style="color: white; position: static;"
      />
      <!-- <h4
        style:color="white"
        style:font-size="1vw"
      >{title}</h4> -->
    </div>
  </div>
{/if}

<style>
  .mapbutton {
    transition: all 0.3s ease-out;
  }

  .mapbutton:hover,
  .mapbutton:focus
  {
    transform: scale(1.25);
    outline: none;
  }
</style>