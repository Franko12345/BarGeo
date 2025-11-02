<script>
  export let text = 'Click me';
  export let variant = 'primary'; // 'primary', 'secondary', 'danger', etc.
  import Sc from "$lib/components/Sc.svelte";

  function handleClick() {
    // Custom logic or emit an event
    console.log(`${text} button clicked!`);
  }

  let color = "#000000";
</script>

<Sc color={color} click={handleClick} enter={() => {color="#222222"; console.log(color)}}
    out={() => {color="#000000"; console.log(color)}}></Sc>

<style>
  button {
    padding: 8px 16px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
</style>
