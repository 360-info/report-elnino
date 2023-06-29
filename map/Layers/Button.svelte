<script>
  import Icon from "@iconify/svelte";
  export let icon;
  export let size = 40;
  export let top;
  export let left;
  export let color = "#666666";
  export let iconScale = 0.6;
  export let deemphasised = false;
</script>

<div
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