<script>
  import { T, useFrame } from '@threlte/core';
  import { OrbitControls, interactivity } from '@threlte/extras'
  import {spring} from 'svelte/motion';
  import { useGltf } from '@threlte/extras';
  import { onMount } from 'svelte';


  let camHeight = 0;
  let statueRotation = 0;

  function moveCamera(){
    const t = document.body.getBoundingClientRect().top;

    camHeight = t * -0.06;
    statueRotation = t * -0.0005;

  }

  interactivity();
  const scale = spring(1);

  let rotation = 0;
  useFrame((state,delta)=>{
    rotation += delta;
  });


  
  onMount(()=>{
    window.addEventListener('scroll',()=>{moveCamera()});
  });


</script>




<T.PerspectiveCamera
  makeDefault
  position={[40,camHeight,1]}
  on:create={({ref})=>
    ref.lookAt(0,-15,0)}
>
<!-- <OrbitControls
enableZoom={true}
enablePan={false}
enableDamping

/> -->

</T.PerspectiveCamera>

<T.DirectionalLight 
  position={[0, 10, 10]} 
  color="#FFD700"
/>

<T.AmbientLight intensity={0.2} />

{#await useGltf('src/lib/model/scene.gltf') then gltf}
  <T is={gltf.scene}
    position={[0,65,0]}
    rotation.y={statueRotation}  
     
  />
{/await}



<!-- <T.Mesh 
  rotation.y={rotation}
  position.y={1}
  scale={$scale}
  castShadow
  on:pointerenter={() => scale.set(1.5)}
  on:pointerleave={() => scale.set(1)}
  >
    <T.BoxGeometry args={[2,2,2]}/>
    <T.MeshStandardMaterial color="orange"/>
</T.Mesh>

<T.Mesh 
  rotation.x={-Math.PI/2} 
  receiveShadow
  position.y={-1}>
  <T.CircleGeometry args={[4, 40]}/>
  <T.MeshStandardMaterial color="white" />
</T.Mesh> -->

