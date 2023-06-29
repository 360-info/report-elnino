<script>
  import { createEventDispatcher } from "svelte";
  import Icon from "@iconify/svelte";

  export let icon;
  export let size = 40;
  export let top;
  export let left;
  export let color = "#666666";
  export let iconScale = 0.6;
  export let deemphasised = false;

  // id, title and description passed back to global state on click
  export let buttonID;
  export let title = "";
  export let description = "";

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

<div
  on:click={activateButton}
  on:keyup={onKeyUp}
  class="mapbutton"
  class:deemphasised
  tabindex="0"
  style:width={size + "px"}
  style:height={size + "px"}
  style:top={top}
  style:left={left}
  style:position="absolute"
  style:background-color={color}
  style:border-radius="50%"
  style:display="flex"
  style:justify-content="center"
  style:align-items="center"
  style:text-align="center"
  style:box-shadow="5px 5px 40px -10px {color}"
  >
  <Icon
    icon={icon}
    width={size * iconScale}  
    style="color: white; position: static;"
   />
</div>

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

  .deemphasised {
    filter: grayscale(50%) opacity(25%);
  }
</style>