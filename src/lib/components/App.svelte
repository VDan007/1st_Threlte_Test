<script>
  import { Canvas } from '@threlte/core';
  import Scene from './Scene.svelte';
  // import { onMount } from 'svelte';
  

 
  


</script>


<div
     
  >
  <Canvas>
    <Scene />
  </Canvas>

</div>
  

<style>
  div{
    position:fixed;
    top:0;
    left:0;
    display:flex;
    justify-content: center;
    width: 100vw;
    height: 100vh;
    z-index: 1;
    
  }
</style>

