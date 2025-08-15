<script lang="ts">
  import ImageSection from '$lib/ImageSection.svelte';
  
  // Sample images array - you can modify this to include your actual images
  const images = [
    {
      src: '/favicon.png',
      alt: 'Website Favicon',
      caption: 'LunexWeb Favicon',
      width: 64,
      height: 64
    },
    {
      src: '/images/optimized/placeholder.jpg',
      alt: 'Sample Image 1',
      caption: 'Sample Image Description',
      width: 300,
      height: 200
    },
    {
      src: '/images/optimized/placeholder2.jpg',
      alt: 'Sample Image 2',
      caption: 'Another Sample Image',
      width: 300,
      height: 200
    }
  ];
</script>

<svelte:head>
  <title>Images - LunexWeb</title>
  <meta name="description" content="View our collection of images including favicon and portfolio work" />
</svelte:head>

<div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100">
  <div class="container mx-auto px-4 py-8">
    <div class="text-center mb-8">
      <h1 class="text-4xl font-bold text-gray-800 mb-4">Image Gallery</h1>
      <p class="text-lg text-gray-600 max-w-2xl mx-auto">
        Explore our collection of images, including our website favicon and portfolio work.
      </p>
    </div>
    
    <ImageSection title="Our Images" {images} />
    
    <div class="mt-12 text-center">
      <h3 class="text-2xl font-semibold text-gray-800 mb-4">Add More Images</h3>
      <p class="text-gray-600 mb-6">
        To add more images to this gallery, place them in the <code class="bg-gray-200 px-2 py-1 rounded">static/images/</code> directory
        and update the images array in this component.
      </p>
      <div class="bg-blue-50 border border-blue-200 rounded-lg p-4 max-w-2xl mx-auto">
        <h4 class="font-semibold text-blue-800 mb-2">Quick Setup:</h4>
        <ol class="text-left text-blue-700 space-y-1">
          <li>1. Place your images in <code class="bg-blue-100 px-1 rounded">static/images/</code></li>
          <li>2. Update the <code class="bg-blue-100 px-1 rounded">images</code> array in this file</li>
          <li>3. Your images will automatically appear in the gallery</li>
        </ol>
      </div>
    </div>
  </div>
</div> 