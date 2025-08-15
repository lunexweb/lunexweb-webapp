<script>
  export let title = "Images";
  export let images = [];
</script>

<section class="image-section py-12 bg-gray-50">
  <div class="container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center mb-8 text-gray-800">
      {title}
    </h2>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      {#each images as image}
        <div class="image-card bg-white rounded-lg shadow-md overflow-hidden hover:shadow-lg transition-shadow duration-300">
          <div class="image-container p-4">
            <img
              src={image.src}
              alt={image.alt}
              width={image.width || 300}
              height={image.height || 200}
              class="w-full h-auto object-cover rounded-md"
              loading="lazy"
            />
          </div>
          {#if image.caption}
            <div class="px-4 pb-4">
              <p class="text-sm text-gray-600 text-center">{image.caption}</p>
            </div>
          {/if}
        </div>
      {/each}
    </div>
    
    {#if images.length === 0}
      <div class="text-center py-8">
        <p class="text-gray-500">No images to display</p>
      </div>
    {/if}
  </div>
</section>

<style>
  .image-section {
    min-height: 400px;
  }
  
  .image-card {
    transition: transform 0.2s ease-in-out;
  }
  
  .image-card:hover {
    transform: translateY(-2px);
  }
</style> 