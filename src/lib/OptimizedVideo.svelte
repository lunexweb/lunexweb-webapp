<script>
  import { onMount } from 'svelte';
  
  export let src = '';
  export let poster = '';
  export let autoplay = true;
  export let muted = true;
  export let loop = true;
  export let playsinline = true;
  export let preload = 'auto';
  export let class_name = '';
  export let objectFit = 'cover';
  export let objectPosition = 'center';
  
  let videoElement;
  let isLoaded = false;
  let hasError = false;
  
  onMount(() => {
    if (videoElement && autoplay) {
      // Ensure video can autoplay
      videoElement.play().catch(error => {
        console.warn('Autoplay prevented:', error);
        hasError = true;
      });
    }
  });
  
  function handleLoad() {
    isLoaded = true;
  }
  
  function handleError() {
    hasError = true;
  }
</script>

{#if src}
  <video
    bind:this={videoElement}
    {src}
    {poster}
    {autoplay}
    {muted}
    {loop}
    {playsinline}
    {preload}
    class={class_name}
    style="object-fit: {objectFit}; object-position: {objectPosition};"
    on:loadeddata={handleLoad}
    on:error={handleError}
  >
    <track kind="captions" />
    Your browser does not support the video tag.
  </video>
  
  {#if !isLoaded && !hasError}
    <!-- Loading state -->
    <div class="absolute inset-0 bg-gray-900/50 flex items-center justify-center">
      <div class="animate-spin rounded-full h-12 w-12 border-b-2 border-white"></div>
    </div>
  {/if}
  
  {#if hasError}
    <!-- Error fallback -->
    <div class="absolute inset-0 bg-gray-900 flex items-center justify-center">
      <div class="text-center text-white">
        <svg class="w-16 h-16 mx-auto mb-4 opacity-50" fill="none" stroke="black" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z" />
        </svg>
        <p class="text-lg">Video unavailable</p>
      </div>
    </div>
  {/if}
{/if}

<style>
  video {
    width: 100%;
    height: 100%;
  }
</style> 