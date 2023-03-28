<script>
    import Geolocation from "svelte-geolocation";

    let coords = [];
    let position;

    let videoSource = null;
    let loading = false;
    const obtenerVideoCamara = async () => {
      try {
        loading = true;
        const stream = await navigator.mediaDevices.getUserMedia({
          video: true,
        });
        videoSource.srcObject = stream;
        videoSource.play();
        loading = false;
      } catch (error) {
        console.log(error);
      }
    };
  </script>
  
  <div>
    <Geolocation getPosition bind:coords />

    <pre>{JSON.stringify(coords)}</pre>
    
    {#if loading}
      <h1>CARGANDO</h1>
    {/if}
    <!-- svelte-ignore a11y-media-has-caption -->
    <video bind:this={videoSource} />
    <button on:click={obtenerVideoCamara}>CLICK</button>
  </div>